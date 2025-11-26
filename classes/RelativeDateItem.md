# RelativeDateItem Documentation

[← Back to API Index](../reference.md)

---

## Class: RelativeDateItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
A FormItem for entering a date relative to today or relative to some other date, or a specific absolute date. Typically used for filtering data by date.

The RelativeDateItem consists of a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) where the user may directly choose one of several [preset options](#attr-relativedateitempresetoptions), choose to enter a [quantity](#attr-relativedateitemquantityfield) and [time unit](../reference_2.md#type-timeunit) (eg "4 months ago" or "3 years from now") or directly type in an absolute date value (7/18/2009).

This item can work with logical dates or datetimes, depending on the specified [data-type](DataSourceField.md#attr-datasourcefieldtype). For detailed information on working with dates, times and datetimes, see the [Date and Time Format and Storage overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

---
## Attr: RelativeDateItem.minQuantity

### Description
Minimum value to allow in the [RelativeDateItem.quantityField](#attr-relativedateitemquantityfield).

**Flags**: IR

---
## Attr: RelativeDateItem.monthsFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "month".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.pickerIconPrompt

### Description
Prompt to show when the user hovers the mouse over the picker icon for this RelativeDateItem. May be overridden for localization of your application.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.shouldSaveValue

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
## Attr: RelativeDateItem.yearsFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "year".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.baseDate

### Description
Base date for calculating the relative date entered by the user.

The default is to use the current date.

**Flags**: IR

---
## Attr: RelativeDateItem.operator

### Description
What operator to use when [RelativeDateItem.getCriterion](#method-relativedateitemgetcriterion) is called.

**Flags**: IR

---
## Attr: RelativeDateItem.rangePosition

### Description
Does this item's relative date value refer to the start or end of the chosen date? Useful when using this item to generate filter criteria, such as the from or to value for an inclusive range.

If unset "start" is assumed.

### See Also

- [RelativeDateItem.operator](#attr-relativedateitemoperator)
- [RelativeDateItem.rangeRoundingGranularity](#attr-relativedateitemrangeroundinggranularity)

**Flags**: IRWA

---
## Attr: RelativeDateItem.daysFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "day".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.dateFormatter

### Description
Format for displaying dates in the [RelativeDateItem.valueField](#attr-relativedateitemvaluefield) and [RelativeDateItem.calculatedDateField](#attr-relativedateitemcalculateddatefield). If unset a default DateDisplayFormat will be picked up from [DynamicForm.dateFormatter](DynamicForm.md#attr-dynamicformdateformatter) (or [DynamicForm.datetimeFormatter](DynamicForm.md#attr-dynamicformdatetimeformatter) for datetime fields} or otherwise from the system-wide default established by [DateUtil.setShortDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdisplayformat), or if this item has its type specified as datetime, [DateUtil.setShortDatetimeDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat).

Note: if entirely custom date formatting/parsing logic is required for this item, this attribute may be set to a custom formatting function. In this case the function will be applied to the Date being formatted (for example `this.getFullYear()` would give you back the full year), and should return the formatted date string.

**Flags**: IR

---
## Attr: RelativeDateItem.valueField

### Description
[ComboBoxItem](ComboBoxItem.md#class-comboboxitem) field where a user may choose among [presets](#attr-relativedateitempresetoptions), [time unit](../reference_2.md#type-timeunit) plus [quantity](#attr-relativedateitemquantityfield), or direct entry of a date as text.

**Flags**: IR

---
## Attr: RelativeDateItem.calculatedDateField

### Description
Field that shows the current calculated date by adding the user-entered relative date to the [RelativeDateItem.baseDate](#attr-relativedateitembasedate).

**Flags**: IR

---
## Attr: RelativeDateItem.pickerIcon

### Description
Icon that launches a [DateChooser](DateChooser.md#class-datechooser) for choosing an absolute date.

**Flags**: IR

---
## Attr: RelativeDateItem.monthsAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "month".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.pickerConstructor

### Description
SmartClient class for the [dateChooser](DateChooser.md#class-datechooser) autoChild displayed to allow the user to directly select dates.

**Flags**: IR

---
## Attr: RelativeDateItem.minutesFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "minute".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.showCalculatedDateField

### Description
Should the Calculated-Date be displayed to the right of the [RelativeDateItem.pickerIcon](#attr-relativedateitempickericon).

**Flags**: IRW

---
## Attr: RelativeDateItem.defaultValue

### Description
Default value to show. Can be a concrete Date, a [RelativeDateString](../reference_2.md#type-relativedatestring) that matches one of the [RelativeDateItem.presetOptions](#attr-relativedateitempresetoptions), or one of the available [time units](#attr-relativedateitemtimeunitoptions). If setting a [TimeUnit](../reference_2.md#type-timeunit), use [defaultQuantity](#attr-relativedateitemdefaultquantity) to establish a default value for the [quantityField](#attr-relativedateitemquantityfield).

**Flags**: IR

---
## Attr: RelativeDateItem.valueFieldWidth

### Description
The [width](FormItem.md#attr-formitemwidth) for the [valueField](#attr-relativedateitemvaluefield) in this item. Defaults to the current default value for the width attribute on the [DateTimeItem](DateTimeItem.md#class-datetimeitem) class - this is assumed to be just wide enough to show a full datetime string, in the current global datetime format.

Setting the width globally on the [DateTimeItem](DateTimeItem.md#class-datetimeitem) class results in all text-based datetime entry fields assuming the same default width - this caters for custom date-time formatters that need differing amounts of space.

**Flags**: IRW

---
## Attr: RelativeDateItem.useSharedPicker

### Description
When set to true (the default), use a single shared date-picker across all widgets that use one. When false, create a new picker using the autoChild system. See [picker](DateItem.md#attr-dateitempickerdefaults) and [pickerProperties](DateItem.md#attr-dateitempickerproperties) for details on setting up an unshared picker.

**Flags**: IR

---
## Attr: RelativeDateItem.secondsFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "second".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.quartersFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "quarter".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.use24HourTime

### Description
When showing the [DateChooser](DateChooser.md#class-datechooser), should the [time field](DateChooser.md#attr-datechoosershowtimeitem) be set to use 24-hour time? Has no effect for fields of type `"date"` rather than `"datetime"`, or if [RelativeDateItem.showPickerTimeItem](#attr-relativedateitemshowpickertimeitem) is `false`.

Default is true.

**Flags**: IRW

---
## Attr: RelativeDateItem.secondsAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "second".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.showPastOptions

### Description
Should we show time-unit options in the past? If set to false, for each [timeUnitOption](#attr-relativedateitemtimeunitoptions) we will show only future options \[for example "N weeks from now"\].

Note: this does not change the [RelativeDateItem.presetOptions](#attr-relativedateitempresetoptions), which show up in addition to the time-unit options (_"N days from now"_, etc). The default preset options include both past and future presets so developers may wish to modify the presets to ensure only past options are available.

**Flags**: IR

---
## Attr: RelativeDateItem.daysAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "day".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.weeksFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "week".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.centuryThreshold

### Description
Only used if we're showing the date in a text field. When parsing a date, if the year is specified with 1 or 2 digits and is less than the centuryThreshold, then the year will be assumed to be 20xx; otherwise it will be interpreted according to default browser behavior, which will consider it to be 19xx.

By default, the _centuryThreshold_ is calculated as the current year + 25.

If you need to allow 1 and 2 digit years, set this attribute to `null` to have the control retain your year-value as entered.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RelativeDateItem.allowAbsoluteDates

### Description
When set to false, only relative dates can be entered - in this mode, the [date chooser icon](#attr-relativedateitemshowchoosericon) is hidden and the [value field](#attr-relativedateitemvaluefield) is switched from a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem), which allows text-entry, to a [SelectItem](SelectItem.md#class-selectitem) which does not.

**Flags**: IR

---
## Attr: RelativeDateItem.yearsAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "year".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.quartersAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "quarter".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.endDate

### Description
Limits the range of the popup [DateChooser](DateChooser.md#class-datechooser).

If unset, the item's popup [DateChooser](FormItem.md#attr-formitempicker) is limited by [DateChooser.endYear](DateChooser.md#attr-datechooserendyear).

Note that changing this attribute after the item is drawn may result in item-validation.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RelativeDateItem.minutesAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "minute".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.rangeRoundingGranularity

### Description
A map from a granularity of time specified by a user to the granularity of time used for rounding.

A relative date such as "n days from now" is normally shifted to the end of the day when used as a range endpoint, and the beginning of the day when used as the beginning of a range. (The rounding direction on some items can be specified via [RelativeDateItem.rangePosition](#attr-relativedateitemrangeposition)). This causes the intuitive behavior that "from yesterday to today" is from the beginning of yesterday to the end of today, and that "from today until 5 days from now" includes the entirety of Friday if today is Monday.

This same rule _can_ be applied to any time granularity, such that "from now until 20 minutes from now" is up to 5:32 if it is now 5:11:34, and "from now until 2 months from now" means end of June if it is mid-April.

User intuitions about where this rounding is expected for any given time period tend to vary based on what kind of event is being discussed and subtle phrasing differences (consider "up to one year from now", "until next year", "within the next couple of years"). The defaults behaviors are:

*   for days, weeks and months round to **day** end/beginning
*   for hours, round to **minute** end/beginning
*   for minutes and seconds, round to **second** end/beginning

To customize this rounding behavior, this attribute may be set to a simple javascript object mapping each timeUnit to the granularity for that timeUnit.  
For example the following config code would produce an item where the user could select only day or week values, and the selected value would be rounded to the beginning of the day if a day was selected, or the beginning of the week if a week was selected:
```
  {
      name:"fromDate", type:"RelativeDateItem",
      timeUnitOptions:["day", "week"],
      rangePosition:"start",
      rangeRoundingGranularity:{
          "day":"day",
          "week":"week"
      }
  }
 
```

**Flags**: IRWA

---
## Attr: RelativeDateItem.showChooserWeekPicker

### Description
When set to true, show a button that allows the calendar to be navigated by week or fiscal week, depending on the value of [RelativeDateItem.showChooserFiscalYearPicker](#attr-relativedateitemshowchooserfiscalyearpicker).

**Flags**: IRW

---
## Attr: RelativeDateItem.timeUnitOptions

### Description
List of time units that will be offered for relative dates.

Each available time unit option will cause two options to appear in the [RelativeDateItem.valueField](#attr-relativedateitemvaluefield). For example, if "day" is an available [time unit](../reference_2.md#type-timeunit) option, there will be ["N days ago"](#attr-relativedateitemdaysagotitle) and ["N days from now"](#attr-relativedateitemdaysfromnowtitle).

### See Also

- [RelativeDateItem.showPastOptions](#attr-relativedateitemshowpastoptions)
- [RelativeDateItem.showFutureOptions](#attr-relativedateitemshowfutureoptions)
- [RelativeDateItem.rangeRoundingGranularity](#attr-relativedateitemrangeroundinggranularity)

**Flags**: IR

---
## Attr: RelativeDateItem.maxQuantity

### Description
Maximum value to allow in the [RelativeDateItem.quantityField](#attr-relativedateitemquantityfield). Increasing this value may result in date miscalculations for very large numbers, due to Javascript Date limitations.

**Flags**: IR

---
## Attr: RelativeDateItem.showFutureOptions

### Description
Should we show time-unit options in the future? If set to false, for each [timeUnitOption](#attr-relativedateitemtimeunitoptions) we will show only past options \[for example "N weeks ago"\].

Note: this does not change the [RelativeDateItem.presetOptions](#attr-relativedateitempresetoptions), which show up in addition to the time-unit options (_"N days from now"_, etc). The default preset options include both past and future presets so developers may wish to modify the presets to ensure only future options are available.

**Flags**: IR

---
## Attr: RelativeDateItem.millisecondsAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "millisecond".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.generateValidator

### Description
When this item has a [startDate](#attr-relativedateitemstartdate) or [endDate](#attr-relativedateitemenddate) specified, should it automatically generate a client-side [dateRange validator](FormItem.md#attr-formitemvalidators) to enforce them?

When true, the default, the item will generate a dateRange validator automatically if the developer hasn't installed one but has set either date-range value.

If a dateRange validator already exists, this attribute is non-functional - no automatic validator is generated, and no checks are made that the values in the developer-provided validator match the item's current start or end dates.

Note that the validator generated by this attribute exists only on the FormItem, so it doesn't do any server enforcement and doesn't cause validation to happen in any other circumstance (eg, an unrelated grid used for editing). For consistent and pervasive enforcement, the validator should be declared on the [DataSourceField](../reference_2.md#object-datasourcefield).

**Flags**: IR

---
## Attr: RelativeDateItem.defaultQuantity

### Description
Default quantity to show in the [RelativeDateItem.quantityField](#attr-relativedateitemquantityfield).

**Flags**: IR

---
## Attr: RelativeDateItem.pickerTimeItemProperties

### Description
A set of properties to apply to the [TimeItem](TimeItem.md#class-timeitem) displayed in the picker when [RelativeDateItem.showPickerTimeItem](#attr-relativedateitemshowpickertimeitem) is true.

Has no effect for fields of type `"date"`.

**Flags**: IRWA

---
## Attr: RelativeDateItem.startDate

### Description
Limits the range of the popup [DateChooser](DateChooser.md#class-datechooser).

If unset, the item's popup [DateChooser](FormItem.md#attr-formitempicker) is limited by [DateChooser.startYear](DateChooser.md#attr-datechooserstartyear).

Note that changing this attribute after the item is drawn may result in item-validation.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RelativeDateItem.showChooserFiscalYearPicker

### Description
When set to true, show a button that allows the calendar to be navigated by fiscal year.

**Flags**: IRW

---
## Attr: RelativeDateItem.presetOptions

### Description
Preset relative dates, such as "today" or "tomorrow", that the user can choose directly from the [RelativeDateItem.valueField](#attr-relativedateitemvaluefield).

Format is an Object mapping user-visible titles to [RelativeDateShortcut](../reference.md#type-relativedateshortcut) or [RelativeDateString](../reference_2.md#type-relativedatestring)s. The default value (expressed in JSON) is:

```
 {
     "$today" : "Today",
     "$yesterday" : "Yesterday",
     "$tomorrow" : "Tomorrow",
     "$weekAgo" : "Current day of last week",
     "$weekFromNow" : "Current day of next week",
     "$monthAgo" : "Current day of last month",
     "$monthFromNow" : "Current day of next month"
 }
 
```
In addition to these presets, options are shown for each of the [timeUnit options](../reference_2.md#type-timeunit).

**Flags**: IR

---
## Attr: RelativeDateItem.showChooserIcon

### Description
Should we show the icon that displays a date-chooser?

**Flags**: IR

---
## Attr: RelativeDateItem.showPickerTimeItem

### Description
If this item is editing a field of type `"datetime"`, should the [DateChooser](DateChooser.md#class-datechooser) display the [time field](DateChooser.md#attr-datechoosershowtimeitem), allowing the user to select a time?

One case where developers will wish to suppress this time-field from being displayed is if a custom [RelativeDateItem.dateFormatter](#attr-relativedateitemdateformatter) has been specified which does not display the time portion of the selected date. In this case any value selected from the DateChooser's time field will be discarded when the picker is dismissed, making it a confusing UI for the end user.

Has no effect if the field type is `"date"` - in this case the picker will never show the time field.

**Flags**: IRWA

---
## Attr: RelativeDateItem.hoursAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "hour".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.weeksAgoTitle

### Description
The title to show for historical periods when the [TimeUnit](../reference_2.md#type-timeunit) is "week".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.hoursFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "hour".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: RelativeDateItem.inputFormat

### Description
Format for direct user input of date values.

If unset, the input format will be determined based on the specified [RelativeDateItem.dateFormatter](#attr-relativedateitemdateformatter) if possible, otherwise picked up from the Date class (see [DateUtil.setInputFormat](DateUtil.md#classmethod-dateutilsetinputformat)).

Note: if entirely custom date formatting/parsing logic is required for this item, this attribute may be set to a function which takes a single parameter (the formatted date string) and returns a JavaScript date object.

**Flags**: IR

---
## Attr: RelativeDateItem.quantityField

### Description
Field allowing user to pick units of time, eg, number of days.

**Flags**: IR

---
## Attr: RelativeDateItem.millisecondsFromNowTitle

### Description
The title to show for future periods when the [TimeUnit](../reference_2.md#type-timeunit) is "millisecond".

### Groups

- i18nMessages

**Flags**: IR

---
## ClassMethod: RelativeDateItem.getAbsoluteDate

### Description
Converts a [RelativeDate](../reference.md#object-relativedate), [RelativeDateShortcut](../reference.md#type-relativedateshortcut), or [RelativeDateString](../reference_2.md#type-relativedatestring) to a concrete Date.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| relativeDate | [RelativeDate](#type-relativedate) | false | — | the relative date to convert |
| baseDate | [Date](#type-date) | true | — | base value for conversion. Defaults to today |

### Returns

`[Date](#type-date)` — resulting absolute date value

---
## Method: RelativeDateItem.getFiscalCalendar

### Description
Returns the [FiscalCalendar](../reference.md#object-fiscalcalendar) object that will be used by this item's DateChooser.

### Returns

`[FiscalCalendar](#type-fiscalcalendar)` — the fiscal calendar for this chooser, if set, or the global one otherwise

---
## Method: RelativeDateItem.setFiscalCalendar

### Description
Sets the [FiscalCalendar](../reference.md#object-fiscalcalendar) object that will be used by this item's DateChooser. If unset, the [global fiscal calendar](DateUtil.md#classmethod-dateutilgetfiscalcalendar) is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the fiscal calendar for this chooser, if set, or the global one otherwise |

---
## Method: RelativeDateItem.getInputFormat

### Description
If [DateItem.useTextField](DateItem.md#attr-dateitemusetextfield) is `true` this method returns a standard [DateInputFormat](../reference.md#type-dateinputformat), determining how values entered by the user are to be converted to Javascript Date objects.

If an explicit [DateItem.inputFormat](DateItem.md#attr-dateiteminputformat) has been specified it will be returned, otherwise, if a custom [DateItem.dateFormatter](DateItem.md#attr-dateitemdateformatter) or [DateItem.format](FormItem.md#attr-formitemformat) are specified, the input format will be automatically derived from that property.

Otherwise, the global [inputFormat](DateUtil.md#classmethod-dateutilsetinputformat) is used.

Note that the inputFormat will ignore any separator characters and padding of values. However if necessary entirely custom date formatting and parsing may be achieved via the [DateItem.formatEditorValue](DateItem.md#method-dateitemformateditorvalue) and [DateItem.parseEditorValue](DateItem.md#method-dateitemparseeditorvalue) methods.

### Returns

`[DateInputFormat](../reference.md#type-dateinputformat)` — expected format of date strings to parse

**Flags**: A

---
## Method: RelativeDateItem.getEnteredValue

### Description
Returns the raw text value typed into this items value text field

---
## Method: RelativeDateItem.getRelativeDate

### Description
Returns the current [RelativeDate](../reference.md#object-relativedate) object for this item. Only applies if the user entered a relative date value (such as "Today") - if an absolute date was entered, this method returns null.  
Relative date objects have the following format:
```
     { _constructor: "RelativeDate", value: "$today" }
 
```

### Returns

`[Object](../reference.md#type-object)` — an object containing the relativeDate string for the current value

---
## Method: RelativeDateItem.parseEditorValue

### Description
RelativeDateItems do not make use of the standard [FormItem.formatEditorValue](FormItem.md#method-formitemformateditorvalue) and [FormItem.parseEditorValue](FormItem.md#method-formitemparseeditorvalue) methods. Developers can customize the display values for these items in the following ways:

*   The [RelativeDateItem.presetOptions](#attr-relativedateitempresetoptions) map allows standard preset RelativeDateString and RelativeDateShortcut values to be mapped to custom display values
*   The text displayed for each of the [RelativeDateItem.timeUnitOptions](#attr-relativedateitemtimeunitoptions) (e.g:"N days ago") may be customized via the per-time unit title attributes ([RelativeDateItem.daysFromNowTitle](#attr-relativedateitemdaysfromnowtitle), [RelativeDateItem.daysAgoTitle](#attr-relativedateitemdaysagotitle), etc)
*   The [RelativeDateItem.dateFormatter](#attr-relativedateitemdateformatter) and [RelativeDateItem.inputFormat](#attr-relativedateiteminputformat) may be used modify how date values are displayed (both in the text entry box and in the [calculatedDateField](#attr-relativedateitemshowcalculateddatefield)

**Flags**: A

---
## Method: RelativeDateItem.formatEditorValue

### Description
RelativeDateItems do not make use of the standard [FormItem.formatEditorValue](FormItem.md#method-formitemformateditorvalue) and [FormItem.parseEditorValue](FormItem.md#method-formitemparseeditorvalue) methods. Developers can customize the display values for these items in the following ways:

*   The [RelativeDateItem.presetOptions](#attr-relativedateitempresetoptions) map allows standard preset RelativeDateString and RelativeDateShortcut values to be mapped to custom display values
*   The text displayed for each of the [RelativeDateItem.timeUnitOptions](#attr-relativedateitemtimeunitoptions) (e.g:"N days ago") may be customized via the per-time unit title attributes ([RelativeDateItem.daysFromNowTitle](#attr-relativedateitemdaysfromnowtitle), [RelativeDateItem.daysAgoTitle](#attr-relativedateitemdaysagotitle), etc)
*   The [RelativeDateItem.dateFormatter](#attr-relativedateitemdateformatter) and [RelativeDateItem.inputFormat](#attr-relativedateiteminputformat) may be used modify how date values are displayed (both in the text entry box and in the [calculatedDateField](#attr-relativedateitemshowcalculateddatefield)

**Flags**: A

---
## Method: RelativeDateItem.getCriterion

### Description
Get the criterion based on the values the user has entered.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| absolute | [boolean](../reference.md#type-boolean) | true | — | whether to use an absolute date in the Criterion produced. By default a [RelativeDate](../reference.md#object-relativedate) will be used if the user entered a relative date value |

### Returns

`[Criterion](#type-criterion)` — —

---
