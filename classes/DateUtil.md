# DateUtil Documentation

[← Back to API Index](../reference.md)

---

## Class: DateUtil

### Description
Static singleton class containing APIs for interacting with Dates.

---
## ClassAttr: DateUtil.shortMonthNames

### Description
This property may be set to an array of shortened month-names.  
For example:
```
 ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
 
```
The appropriate month name will then be returned from [Date.getShortMonthName](Date.md#method-dategetshortmonthname), and may be used whenever SmartClient components display month-names (for example in the [DateItem class](DateItem.md#class-dateitem)).

### Groups

- i18nMessages

**Flags**: IRWA

---
## ClassAttr: DateUtil.monthNames

### Description
This property may be set to an array of names of months.  
For example:
```
 ["January", "February", "March", "April", "May", "June", "July", 
  "August", "September", "October", "November", "December"]
 
```
The appropriate month name will then be returned from [Date.getMonthName](Date.md#method-dategetmonthname), and may be used whenever SmartClient components display month-names (for example in the [DateItem class](DateItem.md#class-dateitem)).

### Groups

- i18nMessages

**Flags**: IRWA

---
## ClassAttr: DateUtil.weekendDays

### Description
Days that are considered "weekend" days. Values should be the integers returned by the JavaScript built-in Date.getDay(), eg, 0 is Sunday and 6 is Saturday. Override to accommodate different workweeks such as Saudi Arabia (Saturday -> Wednesday) or Israel (Sunday -> Thursday).

**Flags**: IR

---
## ClassAttr: DateUtil.shortDayNames

### Description
This property may be set to an array of names of days of the week.  
For example:
```
 ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
 
```
The appropriate day name will then be returned from [Date.getShortDayName](Date.md#method-dategetshortdayname), and may be used whenever SmartClient components display day-names (for example in the [DateItem class](DateItem.md#class-dateitem)).  
Note: For US based applications the first item in the array should be the name for Sunday, then Monday, Tuesday, etc. For browsers with different locales this may vary. To determine the first day for some locale, you can run the following code:
```
    alert(new Date(2000, 0, 2).getDay());
 
```
You should see an alert with a number between zero and 6. This represents the numerical 'day' value for Sunday for your browser's locale, since Jan 2nd 2000 was a Sunday. Therefore if this code alerted the number 6, Sunday should appear last in your list of day-names, and Monday first.

### Groups

- i18nMessages

**Flags**: IRWA

---
## ClassAttr: DateUtil.dayNames

### Description
This property may be set to an array of names of days of the week.  
For example:
```
 ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
 
```
The appropriate day name will then be returned from [Date.getDayName](Date.md#method-dategetdayname) and [DateUtil.getDayNames](#classmethod-dateutilgetdaynames), and may be used whenever SmartClient components display day-names (for example in the [DateItem class](DateItem.md#class-dateitem)).

### Groups

- i18nMessages

**Flags**: IRWA

---
## ClassMethod: DateUtil.combineLogicalDateAndTime

### Description
Combine a logical date (a value appropriate for a DataSourceField of type "date") with a logical time (a value appropriate for a DataSourceField of type "time") into a datetime value (a value appropriate for a DataSourceField of type "datetime")

This method correctly takes into account the current [display timezone](Time.md#classmethod-timesetdefaultdisplaytimezone), specifically, the returned datetime value will show the same date and time as the passed date and time objects when rendered by a SmartClient component that has been configured with a field of type "datetime".

For further background on date, time and datetime types, storage and transmission, see [this overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance representing logical date value |
| time | [Date](#type-date) | false | — | a Date instance representing logical time value |

### Returns

`[Date](#type-date)` — a Date instance representing a datetime value combining the logical date and time passed

---
## ClassMethod: DateUtil.setDefaultDateSeparator

### Description
Sets a new default separator that will be used when formatting dates. By default, this is a forward slash character: "/"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| separator | [String](#type-string) | false | — | separator to use in dates |

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.format

### Description
Return the parameter date formatted according to the parameter [FormatString](../reference.md#type-formatstring). This method is used to implement the [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat) functionality, but it can also be used to format arbitrary dates programmatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | The date to format |
| format | [FormatString](../reference.md#type-formatstring) | false | — | The format to apply to this date |

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.setShowChooserFiscalYearPickers

### Description
Sets the global attribute that dictates whether the [choosers](DateChooser.md#class-datechooser) shelled from [DateItems](DateItem.md#class-dateitem) show a UI for working with Fiscal Years.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showChooserFiscalYearPickers | [boolean](../reference.md#type-boolean) | false | — | whether to show Fiscal Year pickers in DateChoosers by default |

---
## ClassMethod: DateUtil.setShortDatetimeDisplayFormat

### Description
Set the default short format for datetime values. After calling this method, subsequent calls to [Date.toShortDateTime](Date.md#method-datetoshortdatetime) will return a string formatted according to this format specification. Note that this will be the standard datetime format used by SmartClient components.

The `format` parameter may be a [FormatString](../reference.md#type-formatstring), a [DateDisplayFormat](../reference.md#type-datedisplayformat) string, or a function. If passed a function, this function will be executed in the scope of the Date and should return the formatted string.  

Initial default format is `"toUSShortDatetime"`. See [http://en.wikipedia.org/wiki/Date\_format\_by\_country](http://en.wikipedia.org/wiki/Date_format_by_country) for a useful overview of standard date formats per country.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [FormatString](../reference.md#type-formatstring)|[DateDisplayFormat](../reference.md#type-datedisplayformat)|[Function](#type-function) | false | — | new formatter |

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.compareDates

### Description
Compare two dates; returns 0 if equal, -1 if the first date is greater (later), or 1 if the second date is greater. If either value is not a Date object, it is treated as the epoch (midnight on Jan 1 1970) for comparison purposes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date1 | [Date](#type-date) | false | — | first date to compare |
| date2 | [Date](#type-date) | false | — | second date to compare |

### Returns

`[int](../reference.md#type-int)` — 0 if equal, -1 if first date > second date, 1 if second date > first date

---
## ClassMethod: DateUtil.setInputFormat

### Description
Sets up the default system-wide input format for strings being parsed into dates via `DateUtil.parseInput()`. This will effect how SmartClient components showing editable date or datetime fields parse user-entered values into live Date objects.

The input format can be specified as a [DateInputFormat](../reference.md#type-dateinputformat) - a 3 character string like `"MDY"` indicating the order of the Month, Day and Year components of date strings.

As an example - an input format of "MDY" would parse "01/02/1999" to Jan 2nd 1999  
This standard parsing logic will also handle date-time strings such as "01/02/1999 08:45", or "01/02/1999 16:21:05".

Notes:

*   If the inputFormat is not explicitly set,the system automatically determines the standard input format will be based on the specified [DateUtil.shortDisplayFormat](#classmethod-dateutilsetshortdisplayformat) wherever possible. For example if the short display format has been set to "toEuropeanShortDate" the input format will default to "DMY".
*   The default date parsing functionality built into SmartClient will handle dates presented with any separator string, and can handle 1 or 2 digit day and month values, months formatted as [DateUtil.getMonthNames](#classmethod-dateutilgetmonthnames) or [DateUtil.getShortMonthNames](#classmethod-dateutilgetshortmonthnames), and 2 or 4 digit year values. This means that in many cases custom date display formats can be parsed back to Date values without the need for a custom parser function. However if more sophisticated parsing logic is required, a function may be passed into this method. In this case the parser function should be able to handle parsing date and datetime values formatted via [Date.toShortDate](Date.md#method-datetoshortdate) and [Date.toShortDateTime](Date.md#method-datetoshortdatetime).
*   Date parsing and formatting logic may be overridden at the component level by setting properties directly on the component or field in question.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [DateInputFormat](../reference.md#type-dateinputformat)|[Function](#type-function) | false | — | Default format for strings to be parsed into Dates. If this method is passed a function, it is expected to take a single parameter (the formatted date string), and return the appropriate Javascript Date object (or null if appropriate). |

### See Also

- [DateUtil.parseInput](#classmethod-dateutilparseinput)

---
## ClassMethod: DateUtil.getDayNames

### Description
Return an array of the full names of each day, suitable for use in a selection list, etc. Day names are picked up from [DateUtil.dayNames](#classattr-dateutildaynames), which defaults to an array of English-language strings and these are updated to localized values by loading a locale.

If `DateUtil.dayNames` is purposely cleared, this method will fall back to deriving day-names from the native browser date string. Note, if we have to use this native backup behavior, the day names may vary by browser as well as locale - for example, they may be in an abbreviated form, similar to the result of calling [DateUtil.getShortDayNames](#classmethod-dateutilgetshortdaynames).

### Returns

`[Array of String](#type-array-of-string)` — array of day names

### Groups

- dateFormatting

**Flags**: A

---
## ClassMethod: DateUtil.getDefaultDateSeparator

### Description
gets the default date separator string

### Returns

`[String](#type-string)` — the default date separator

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.getFiscalWeek

### Description
Returns a date's week-number, according to the fiscal calendar

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the date to get the fiscal year for |
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the object representing the starts of fiscal years |

### Returns

`[int](../reference.md#type-int)` — the fiscal week for the passed date

---
## ClassMethod: DateUtil.getDisplayDay

### Description
Returns the day of month from the passed datetime, as it will be displayed to the user. This might not be the same value as that returned by getDate() if a [custom timezone](Time.md#classmethod-timesetdefaultdisplaytimezone) has been applied. Only necessary for datetimes - for logical dates and times, this method returns the same value as getDate().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| datetime | [Date](#type-date) | false | — | datetime instance to work with |

### Returns

`[int](../reference.md#type-int)` — the day of month from the passed datetime

---
## ClassMethod: DateUtil.setWeekendDays

### Description
Sets the days that are considered [weekend days](#classattr-dateutilweekenddays). The parameter should be array of the integers returned by the JavaScript built-in Date.getDay(), eg, 0 is Sunday and 6 is Saturday. Override to accommodate different workweeks such as Saudi Arabia (Saturday -> Wednesday) or Israel (Sunday -> Thursday).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| weekendDays | [Array of Integer](#type-array-of-integer) | false | — | the array of day-numbers to assign as weekend days |

---
## ClassMethod: DateUtil.getFiscalYear

### Description
Returns the [FiscalYear](../reference_2.md#object-fiscalyear) object for the fiscal year in which the passed date exists.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date)|[int](../reference.md#type-int) | false | — | the date to get the fiscal year for |
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the object representing the start of the fiscal period |

### Returns

`[FiscalYear](#type-fiscalyear)` — the [FiscalYear](../reference_2.md#object-fiscalyear) object for the passed date

---
## ClassMethod: DateUtil.create

### Description
Create a new `Date` object - synonym for `new Date(arguments)`

### Returns

`[Date](#type-date)` — Date object

---
## ClassMethod: DateUtil.setNormalDisplayFormat

### Description
Set the default formatter for date objects to the method name passed in. After calling this method, subsequent calls to [Date.toNormalDate](Date.md#method-datetonormaldate) will return a string formatted according to this format specification. Note: this will be the standard long date format used by SmartClient components.

The `format` parameter may be a [FormatString](../reference.md#type-formatstring), a [DateDisplayFormat](../reference.md#type-datedisplayformat) string, or a function. If passed a function, this function will be executed in the scope of the Date and should return the formatted string.  

Initial default normalDisplayFormat is `"toLocaleString"`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [FormatString](../reference.md#type-formatstring)|[DateDisplayFormat](../reference.md#type-datedisplayformat)|[Function](#type-function) | false | — | new formatter |

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.compareLogicalDates

### Description
Compare two dates, normalizing out the time elements so that only the date elements are considered; returns 0 if equal, -1 if the first date is greater (later), or 1 if the second date is greater.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date1 | [Date](#type-date) | false | — | first date to compare |
| date2 | [Date](#type-date) | false | — | second date to compare |

### Returns

`[int](../reference.md#type-int)` — 0 if equal, -1 if first date > second date, 1 if second date > first date. Returns false if either argument is not a date

---
## ClassMethod: DateUtil.getLogicalTimeOnly

### Description
Get a logical time - a value appropriate for a DataSourceField of type "time" - from a datetime value (a value from a DataSourceField of type "datetime").

This method correctly takes into account the current [display timezone](Time.md#classmethod-timesetdefaultdisplaytimezone), specifically, the returned Date will reflect the hour, minute and second that appears when the datetime is rendered by a SmartClient component rather than the time values that would be returned by Date.getHours() et al (which can differ, since getHours() uses the browser's local timezone).

For further background on date, time and datetime types, storage and transmission, see [this overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance representing a datetime value |

### Returns

`[Date](#type-date)` — a Date instance representing just the time portion of the datetime value, as a logical time

---
## ClassMethod: DateUtil.getEndOf

### Description
Returns the end of some period, like day, week or month, relative to a passed Date instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the base date to find the period end from |
| period | [String](#type-string) | false | — | the period to return the end of, one of mn/h/d/w/m/y |
| logicalDate | [Boolean](#type-boolean) | true | — | process and return a logicalDate with no time element |
| firstDayOfWeek | [Integer](../reference_2.md#type-integer) | true | — | which day should be considered the firstDayOfWeek - overrides the default provided by the locale |

### Returns

`[Date](#type-date)` — a Date instance representing the end of the period relative to the passed date

**Flags**: A

---
## ClassMethod: DateUtil.setShowChooserWeekPickers

### Description
Sets the global attribute that dictates whether the [choosers](DateChooser.md#class-datechooser) shelled from [DateItems](DateItem.md#class-dateitem) show a UI for working with Weeks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showChooserWeekPickers | [boolean](../reference.md#type-boolean) | false | — | whether to show Fiscal Week pickers in DateChoosers by default |

---
## ClassMethod: DateUtil.setShortDisplayFormat

### Description
Set the default short format for dates. After calling this method, subsequent calls to [Date.toShortDate](Date.md#method-datetoshortdate) will return a string formatted according to this format specification. Note that this will be the standard short date format used by SmartClient components.

The `format` parameter may be a [FormatString](../reference.md#type-formatstring), a [DateDisplayFormat](../reference.md#type-datedisplayformat) string, or a function. If passed a function, this function will be executed in the scope of the Date and should return the formatted string.  

Initial default shortDateFormat is `"toUSShortDate"`. This property is commonly modified for localization of applications. See [http://en.wikipedia.org/wiki/Date\_format\_by\_country](http://en.wikipedia.org/wiki/Date_format_by_country) for a useful overview of standard date formats per country.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [FormatString](../reference.md#type-formatstring)|[DateDisplayFormat](../reference.md#type-datedisplayformat)|[Function](#type-function) | false | — | new formatter |

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.getDisplayMonth

### Description
Returns the month number from the passed datetime, as it will be displayed to the user. This might not be the same value as that returned by getMonth() if a [custom timezone](Time.md#classmethod-timesetdefaultdisplaytimezone) has been applied. Only necessary for datetimes - for logical dates and times, this method returns the same value as getMonth().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| datetime | [Date](#type-date) | false | — | datetime instance to work with |

### Returns

`[int](../reference.md#type-int)` — the month number from the passed datetime

---
## ClassMethod: DateUtil.setFiscalCalendar

### Description
Sets the global fiscal calendar, which is used for all calls to getFiscalYear() / getFiscalWeek() if those methods aren't passed a fiscalCalander.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | false | — | the object representing the start month and date of the fiscal year in the current locale |

---
## ClassMethod: DateUtil.getDisplayMinutes

### Description
Returns the minutes value from the passed datetime, as it will be displayed to the user. This might not be the same value as that returned by getMinutes() if a [custom timezone](Time.md#classmethod-timesetdefaultdisplaytimezone) has been applied. Only necessary for datetimes - for logical dates and times, this method returns the same value as getMinutes().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| datetime | [Date](#type-date) | false | — | datetime instance to work with |

### Returns

`[int](../reference.md#type-int)` — the minutes value from the passed datetime

---
## ClassMethod: DateUtil.getStartOf

### Description
Returns the start of some period, like day, week or month, relative to a passed Date instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | the base date to find the period start from |
| period | [String](#type-string) | false | — | the period to return the start of, one of mn/h/d/w/m/y |
| logicalDate | [Boolean](#type-boolean) | true | — | process and return a logicalDate with no time element |
| firstDayOfWeek | [Integer](../reference_2.md#type-integer) | true | — | which day should be considered the firstDayOfWeek - overrides the default provided by the locale |

### Returns

`[Date](#type-date)` — a Date instance representing the start of the period relative to the passed date

**Flags**: A

---
## ClassMethod: DateUtil.setNormalDatetimeDisplayFormat

### Description
Set the default normal format for datetime values. After calling this method, subsequent calls to [Date.toNormalDatetime](Date.md#method-datetonormaldatetime) will return a string formatted according to this format specification. Note that this will be the standard datetime format used by SmartClient components.

The `format` parameter may be a [FormatString](../reference.md#type-formatstring), a [DateDisplayFormat](../reference.md#type-datedisplayformat) string, or a function. If passed a function, this function will be executed in the scope of the Date and should return the formatted string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [FormatString](../reference.md#type-formatstring)|[DateDisplayFormat](../reference.md#type-datedisplayformat)|[Function](#type-function) | false | — | new formatter |

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.createLogicalTime

### Description
Create a new Date object to represent a logical time value (rather than a specific datetime value), typically for display in a [time type field](DataSourceField.md#attr-datasourcefieldtype). The generated Date value will have year, month and date set to the epoch date (Jan 1 1970), and time elements set to the supplied hour, minute and second (in browser native local time).

For simplicity, you can pass a Date-instance in the first parameter to create a logical time from that Date instance. Passing `null` is the same as passing `new Date()`. When the first parameter is a Date instance, the `minutes` and `seconds` parameters may still be passed to fine-tune the result - for example, `createLogicalTime(null, 0, 0)` will return a Date instance with time-values representing the start of the current hour.

See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on date, time and datetime values in SmartClient.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hour | [Integer](../reference_2.md#type-integer)|[Date](#type-date) | false | — | integer hour (0-23) or a Date instance - if passed a Date instance, its time-elements are mapped to hour, minute and second parameters. Passing null is the same as passing `new Date()` |
| minute | [Integer](../reference_2.md#type-integer) | false | — | minute (0-59) - defaults to zero or, if the `hour` parameter is a Date instance, the minutes from that Date instance |
| second | [Integer](../reference_2.md#type-integer) | false | — | second (0-59) - defaults to zero or, if the `hour` parameter is a Date instance, the seconds from that Date |

### Returns

`[Date](#type-date)` — new Javascript Date object representing the time in question

---
## ClassMethod: DateUtil.parseInput

### Description
Parse a date passed in as a string, returning the appropriate date object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dateString | [String](#type-string) | false | — | date value as a string |
| format | [DateInputFormat](../reference.md#type-dateinputformat) | true | — | Format of the date string being passed. If not passed, the default date input format as set up via setInputFormat() will be used. |
| centuryThreshold | [Integer](../reference_2.md#type-integer) | true | — | For date formats that support a 2 digit year, if parsed year is 2 digits and less than this number, assume year to be 20xx rather than 19xx |
| suppressConversion | [Boolean](#type-boolean) | true | — | If the string passed in was not a valid date, in some cases we can convert to a valid date (for example incrementing the year if the month is greater than 12). This optional parameter will suppress such conversions - anything that doesn't parse directly to a valid date will simply return null. |

### Returns

`[Date](#type-date)` — date value, or null if the string could not be parsed to a valid date.

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.createLogicalDate

### Description
Create a new Date to represent a logical date value (rather than a specific datetime value), typically for display in a [date type field](DataSourceField.md#attr-datasourcefieldtype). The generated Date value will have year, month and date set to the specified values (in browser native local time).

For simplicity, you can pass a Date-instance in the first parameter to create a logical version of it. Passing `null` is the same as passing `new Date()`. When the first parameter is a Date instance, the `month` and `date` parameters may still be passed to fine-tune the result - for example, `createLogicalDate(null, null, 1)` will return a Date instance representing the first day of the current month.

See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on date, time and datetime values in SmartClient.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| year | [int](../reference.md#type-int)|[Date](#type-date) | false | — | full year or a Date instance - if passed a Date, its parts are mapped to year, month and date parameters. Passing null is the same as passing `new Date()` |
| month | [int](../reference.md#type-int) | false | — | month (zero based, so 0 is January) - defaults to today's month or, if the `year` parameter is a Date instance, to the month from that instance |
| date | [int](../reference.md#type-int) | false | — | date within the month - defaults to today's date or, if the `year` parameter is a Date instance, to the date from that instance |

### Returns

`[Date](#type-date)` — new javascript Date object representing the Date in question

---
## ClassMethod: DateUtil.adjustDate

### Description
Returns a new [Date](../reference_2.md#object-date) instance, representing the `baseDate` adjusted by the relative amount of the [relativeDateString](../reference_2.md#type-relativedatestring).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| baseDate | [Date](#type-date) | false | — | Date instance to apply a relative amount to - defaults to new Date() |
| relativeDateString | [RelativeDateString](../reference_2.md#type-relativedatestring) | false | — | the relative amount to apply to the `baseDate` |

### Returns

`[Date](#type-date)` — a new Date instance representing the `baseDate` adjusted by the `relativeDateString`

---
## ClassMethod: DateUtil.mapRelativeDateShortcut

### Description
Converts a [RelativeDateShortcut](../reference.md#type-relativedateshortcut) to a [RelativeDateString](../reference_2.md#type-relativedatestring).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| relativeDate | [RelativeDateShortcut](../reference.md#type-relativedateshortcut) | false | — | shortcut string to convert |
| rangePosition | [RelativeDateRangePosition](../reference_2.md#type-relativedaterangeposition) | true | — | Are we interested in the start or end of the specified relative date? This applies to shortcuts which do not specify a specific moment (such as `$today`) - it does not apply to shortcuts which already specify a specific moment such as `$startOfToday`. If unspecified rangePosition is always assumed to be "start" |

### Returns

`[RelativeDateString](../reference_2.md#type-relativedatestring)` — converted relative date string.

**Flags**: A

---
## ClassMethod: DateUtil.getDisplayHours

### Description
Returns the hours value from the passed datetime, as it will be displayed to the user. This might not be the same value as that returned by getHours() if a [custom timezone](Time.md#classmethod-timesetdefaultdisplaytimezone) has been applied. Only necessary for datetimes - for logical dates and times, this method returns the same value as getHours().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| datetime | [Date](#type-date) | false | — | datetime instance to work with |

### Returns

`[int](../reference.md#type-int)` — the hours value from the passed datetime

---
## ClassMethod: DateUtil.getWeekendDays

### Description
Return an array of days that are considered "weekend" days. Values will be the integers returned by the JavaScript built-in Date.getDay(), eg, 0 is Sunday and 6 is Saturday. Override [DateUtil.weekendDays](#classattr-dateutilweekenddays) to accommodate different workweeks such as Saudi Arabia (Saturday -> Wednesday) or Israel (Sunday -> Thursday).

### Returns

`[Array of Integer](#type-array-of-integer)` — array of weekend days

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.createDatetime

### Description
Create a new Date object in the current locale time, typically for display in a [datetime field](DataSourceField.md#attr-datasourcefieldtype).

For simplicity, you can pass a Date-instance in the first parameter to create a new date from that Date instance. If you pass a date-string, it is converted to a Date instance. Passing `null` is the same as passing `new Date()`. When the first parameter is a Date instance or string, the various datetime-element parameters - month, hour, etc - may still be passed to fine-tune the result.

See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on date, time and datetime values in SmartClient.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| year | [Integer](../reference_2.md#type-integer)|[Date](#type-date) | true | — | full year or a Date instance or date-string - if passed a Date, or a date-string, its parts are mapped to all the other parameters. Passing null is the same as passing `new Date()` |
| month | [Integer](../reference_2.md#type-integer) | true | — | month (zero based, so 0 is January) - defaults to today's month or, if the `year` parameter is a Date instance, to the month from that instance |
| date | [Integer](../reference_2.md#type-integer) | true | — | date within the month - defaults to today's date or, if the `year` parameter is a Date instance, to the date from that instance |
| hour | [Integer](../reference_2.md#type-integer) | true | — | integer hour (0-23) - defaults to zero or, if the `year` parameter is a Date instance, the hours from that Date instance |
| minute | [Integer](../reference_2.md#type-integer) | true | — | minute (0-59) - defaults to zero or, if the `year` parameter is a Date instance, the minutes from that Date instance |
| second | [Integer](../reference_2.md#type-integer) | true | — | second (0-59) - defaults to zero or, if the `year` parameter is a Date instance, the seconds from that Date |

### Returns

`[Date](#type-date)` — new Javascript Date object representing the time in question in the current locale time

---
## ClassMethod: DateUtil.getDisplayYear

### Description
Returns the full year from the passed datetime, as it will be displayed to the user. This might not be the same value as that returned by getFullYear() if a [custom timezone](Time.md#classmethod-timesetdefaultdisplaytimezone) has been applied. Only necessary for datetimes - for logical dates and times, this method returns the same value as getFullYear().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| datetime | [Date](#type-date) | false | — | datetime instance to work with |

### Returns

`[int](../reference.md#type-int)` — the 4-digit display year from the passed datetime

---
## ClassMethod: DateUtil.getLogicalDateOnly

### Description
Get a logical date - a value appropriate for a DataSourceField of type "date" - from a datetime value (a value from a DataSourceField of type "datetime").

This method correctly takes into account the current [display timezone](Time.md#classmethod-timesetdefaultdisplaytimezone), specifically, the returned Date will reflect the day, month and year that appears when the datetime is rendered by a SmartClient component rather than the date values that would be returned by Date.getDay() et al (which can differ, since getDay() uses the browser's local timezone).

For further background on date, time and datetime types, storage and transmission, see [this overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | a Date instance representing a datetime value |

### Returns

`[Date](#type-date)` — a Date instance representing just the date portion of the datetime value, as a logical date

---
## ClassMethod: DateUtil.getInputFormat

### Description
Retrieves the default format for strings being parsed into dates via `DateUtil.parseInput()`

### Returns

`[String](#type-string)` — the current inputFormat for dates

### See Also

- [DateUtil.setInputFormat](#classmethod-dateutilsetinputformat)

---
## ClassMethod: DateUtil.getFiscalStartDate

### Description
Returns the start date of the fiscal year for the passed date.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date)|[number](#type-number) | false | — | the date, or the year-number, to get the fiscal year for |
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the object representing the starts of one or more fiscal years |

### Returns

`[Date](#type-date)` — the start of the fiscal year for the passed date and fiscalCalendar

---
## ClassMethod: DateUtil.getFirstDayOfWeek

### Description
Returns the global attribute that dictates which day should be treated as the first day of the week in calendars and date calculations. The parameter is expected to be an integer value between 0 (Sunday) and 6 (Saturday).

The default value is picked up from the current locale.

### Returns

`[int](../reference.md#type-int)` — the number of the day being used as the first day of the week

---
## ClassMethod: DateUtil.getAbsoluteDate

### Description
Converts a [RelativeDate](../reference.md#object-relativedate), [RelativeDateShortcut](../reference.md#type-relativedateshortcut), or [RelativeDateString](../reference_2.md#type-relativedatestring) to a concrete Date.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| relativeDate | [RelativeDate](#type-relativedate)|[RelativeDateShortcut](../reference.md#type-relativedateshortcut)|[RelativeDateString](../reference_2.md#type-relativedatestring) | false | — | the relative date to convert |
| baseDate | [Date](#type-date) | true | — | base value for conversion. Defaults to the current date/time. |
| rangePosition | [RelativeDateRangePosition](../reference_2.md#type-relativedaterangeposition) | true | — | optional date-range position. Only has an effect if the date passed in is a [RelativeDateShortcut](../reference.md#type-relativedateshortcut) where the range position is not implicit, such as "$yesterday" |
| isLogicalDate | [boolean](../reference.md#type-boolean) | true | — | should the generated date be marked as a "logical" date? A logical date object is a Date value where the time component is ignored for formatting and serialization purposes - such as the date displayed within a component field of specified type "date". See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more on logical dates vs datetime type values. |

### Returns

`[Date](#type-date)` — resulting absolute date value

---
## ClassMethod: DateUtil.getShortDayNames

### Description
Return an array of the short names of each day, suitable for use in a selection list, etc. Day names are picked up from a [DateUtil.shortDayNames](#classattr-dateutilshortdaynames) list specified in each locale.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| length | [int](../reference.md#type-int) | false | — | maximum length of each day string - default is no maximum (full strings) |

### Returns

`[Array of String](#type-array-of-string)` — array of short day names

### Groups

- dateFormatting

**Flags**: A

---
## ClassMethod: DateUtil.getFiscalCalendar

### Description
Returns the global [FiscalCalendar object](../reference.md#object-fiscalcalendar) representing the start month and date of the fiscal year in the current locale.

### Returns

`[FiscalCalendar](#type-fiscalcalendar)` — the FiscalCalendar object

---
## ClassMethod: DateUtil.today

### Description
Return a `logicalDate` representing the current day in the [defaultDisplayTimezone](Time.md#classmethod-timesetdefaultdisplaytimezone).

### Groups

- dateFormatting

---
## ClassMethod: DateUtil.setFirstDayOfWeek

### Description
Sets the global attribute that dictates which day should be treated as the first day of the week in calendars and date calculations. The parameter is expected to be an integer value between 0 (Sunday) and 6 (Saturday).

The default value is picked up from the current locale.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| firstDayOfWeek | [int](../reference.md#type-int) | false | — | the number of the day to use as the first day of the week |

---
