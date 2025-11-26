# Date Documentation

[← Back to API Index](../reference.md)

---

## ClassAttr: Date.weekendDays

### Description
Days that are considered "weekend" days. Values should be the integers returned by the JavaScript built-in Date.getDay(), eg, 0 is Sunday and 6 is Saturday. Override to accommodate different workweeks such as Saudi Arabia (Saturday -> Wednesday) or Israel (Sunday -> Thursday).

**Deprecated**

**Flags**: IR

---
## ClassAttr: Date.shortMonthNames

### Description
This property may be set to an array of shortened month-names.  
For example:
```
 ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
 
```
The appropriate month name will then be returned from [Date.getShortMonthName](#method-dategetshortmonthname), and may be used whenever SmartClient components display month-names (for example in the [DateItem class](DateItem.md#class-dateitem)).

### Groups

- i18nMessages

**Deprecated**

**Flags**: IRWA

---
## ClassAttr: Date.dayNames

### Description
This property may be set to an array of names of days of the week.  
For example:
```
 ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
 
```
The appropriate day name will then be returned from [Date.getDayName](#method-dategetdayname) and [DateUtil.getDayNames](DateUtil.md#classmethod-dateutilgetdaynames), and may be used whenever SmartClient components display day-names (for example in the [DateItem class](DateItem.md#class-dateitem)).

### Groups

- i18nMessages

**Deprecated**

**Flags**: IRWA

---
## ClassAttr: Date.monthNames

### Description
This property may be set to an array of names of months.  
For example:
```
 ["January", "February", "March", "April", "May", "June", "July", 
  "August", "September", "October", "November", "December"]
 
```
The appropriate month name will then be returned from [Date.getMonthName](#method-dategetmonthname), and may be used whenever SmartClient components display month-names (for example in the [DateItem class](DateItem.md#class-dateitem)).

### Groups

- i18nMessages

**Deprecated**

**Flags**: IRWA

---
## Method: Date.toNormalDate

### Description
Returns the date as a formatted string using the format set up via the `setNormalDisplayFormat()` method. Note that the default formatter for this method is `"toLocaleString"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [DateDisplayFormat](../reference.md#type-datedisplayformat) | false | — | Optional Format for the date returned |

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.getShortDayName

### Description
Return the abbreviated (up to 3 chars) day of week name for this date (Mon, Tue, etc). To modify the value returned by this method, set [DateUtil.shortDayNames](DateUtil.md#classattr-dateutilshortdaynames)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| length | [int](../reference.md#type-int) | false | — | Number of characters to return (Defaults to 3, can't be longer than 3) |

### Returns

`[String](#type-string)` — Abbreviated day name

### Groups

- dateFormatting

---
## Method: Date.duplicate

### Description
Copy the value of this date into a new Date() object for independent manipulation

**Flags**: A

---
## Method: Date.toShortDate

### Description
Returns the date as a formatted string using the format set up via the `setShortDisplayFormat()` method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [DateDisplayFormat](../reference.md#type-datedisplayformat) | false | — | Optional Format for the date returned |
| useCustomTimezone | [Boolean](#type-boolean) | true | — | If a custom timezone has been set via Time.setDefaultDisplayTimezone(), by default date formatters will respect this timezone. to suppress this behavior, this parameter should be set to false. |

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.getDefaultDateSeparator

### Description
gets the default date separator string

### Returns

`[String](#type-string)` — the default date separator

### Groups

- dateFormatting

---
## Method: Date.getFiscalWeek

### Description
Returns the fiscal week number of the current date, according to the global [FiscalCalendar](DateUtil.md#classmethod-dateutilsetfiscalcalendar).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the object representing the starts of fiscal years |

### Returns

`[int](../reference.md#type-int)` — the week number, offset from the start of the fiscal period

---
## Method: Date.toNormalDatetime

### Description
Returns the datetime as a formatted string using the format set up via the `setNormalDatetimeDisplayFormat()` method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [DateDisplayFormat](../reference.md#type-datedisplayformat) | false | — | Optional Format for the date returned |
| useCustomTimezone | [Boolean](#type-boolean) | true | — | If a custom timezone has been set via Time.setDefaultDisplayTimezone(), by default date formatters will respect this timezone. To suppress this behavior, this parameter should be set to false. |

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.toDateStamp

### Description
Return this date in the format (UTC timezone): `_YYYYMMDD_T_HHMMSS_[Z]`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.getDayName

### Description
Return the full day of week name for this date (Monday, Tuesday, etc). To modify the value returned by this method, set [DateUtil.dayNames](DateUtil.md#classattr-dateutildaynames)

### Returns

`[String](#type-string)` — Day name

### Groups

- dateFormatting

---
## Method: Date.getShortYear

### Description
Return a 2 digit year for this date.

### Returns

`[String](#type-string)` — year number, padded to 2 characters

### Groups

- dateFormatting

---
## Method: Date.getMonthName

### Description
Return the full name of the month for this date (January, February, etc) To modify the value returned by this method, set [DateUtil.shortMonthNames](DateUtil.md#classattr-dateutilshortmonthnames) .

### Returns

`[String](#type-string)` — Month name

### Groups

- dateFormatting

---
## Method: Date.toUSShortDate

### Description
Return this date in the format: `MM/DD/YYYY`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.setFormatter

### Description
Set the formatter for this date object to the method name passed in. After this call wherever appropriate SmartClient components will use this formatter function to return the date as a string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| functionName | [String](#type-string) | false | — | name of a date formatter method on this Date |

### Groups

- dateFormatting

**Deprecated**

---
## Method: Date.toJapanShortDateTime

### Description
Return this date in the format: `YYYY/MM/DD HH:MM:SS`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.toShortDateTime

### Description
Returns the datetime as a formatted string using the format set up via the `setShortDatetimeDisplayFormat()` method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [DateDisplayFormat](../reference.md#type-datedisplayformat) | false | — | Optional Format for the date returned |
| useCustomTimezone | [Boolean](#type-boolean) | true | — | If a custom timezone has been set via Time.setDefaultDisplayTimezone(), by default date formatters will respect this timezone. to suppress this behavior, this parameter should be set to false. |

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.toEuropeanShortDate

### Description
Return this date in the format: `DD/MM/YYYY`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.getShortMonthName

### Description
Return the abbreviated name of the month for this date (Jan, Feb, etc) To modify the value returned by this method, set [DateUtil.shortMonthNames](DateUtil.md#classattr-dateutilshortmonthnames) .

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| length | [int](../reference.md#type-int) | false | — | Number of characters to return (Defaults to 3, can't be longer than 3) |

### Returns

`[String](#type-string)` — Abbreviated month name (3 character string)

### Groups

- dateFormatting

---
## Method: Date.toSerializeableDate

### Description
Return this date in 'serialized' format `YYYY-MM-DD HH:MM:SS`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

**Flags**: A

---
## Method: Date.getFiscalYear

### Description
Returns the [FiscalYear](../reference_2.md#object-fiscalyear) object appropriate for the the current date, according to the [FiscalCalendar](../reference.md#object-fiscalcalendar).

### Returns

`[FiscalYear](#type-fiscalyear)` — the fiscal year object

---
## Method: Date.toEuropeanShortDateTime

### Description
Return this date in the format: `DD/MM/YYYY HH:MM`.

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.toUSShortDateTime

### Description
Return this date in the format: `MM/DD/YYYY HH:MM`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.setDefaultDateSeparator

### Description
Sets a new default separator that will be used when formatting dates. By default, this is a forward slash character: "/"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| separator | [String](#type-string) | false | — | separator to use in dates |

### Groups

- dateFormatting

---
## Method: Date.toJapanShortDate

### Description
Return the date in this format: `YYYY/MM/DD`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

---
## Method: Date.getWeek

### Description
Returns an integer containing the week number.

### Returns

`[int](../reference.md#type-int)` — week number, starting with 1

### Groups

- dateFormatting

---
## Method: Date.toPrettyString

### Description
Return this date in the format: `MM/DD/YY HH:MM`

### Returns

`[String](#type-string)` — formatted date string

### Groups

- dateFormatting

**Deprecated**

---
## StaticMethod: Date.setFirstDayOfWeek

### Description
Sets the global attribute that dictates which day should be treated as the first day of the week in calendars and date calculations. The parameter is expected to be an integer value between 0 (Sunday) and 6 (Saturday).

The default value is picked up from the current locale.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| firstDayOfWeek | [int](../reference.md#type-int) | false | — | the number of the day to use as the first day of the week |

**Deprecated**

---
## StaticMethod: Date.setFiscalCalendar

### Description
Sets the global fiscal calendar, which is used for all calls to getFiscalYear() / getFiscalWeek() if those methods aren't passed a fiscalCalander.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | false | — | the object representing the start month and date of the fiscal year in the current locale |

**Deprecated**

---
## StaticMethod: Date.combineLogicalDateAndTime

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

**Deprecated**

---
## StaticMethod: Date.getFiscalYear

### Description
Returns the [FiscalYear](../reference_2.md#object-fiscalyear) object for the fiscal year in which the passed date exists.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date)|[int](../reference.md#type-int) | false | — | the date to get the fiscal year for |
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the object representing the start of the fiscal period |

### Returns

`[FiscalYear](#type-fiscalyear)` — the [FiscalYear](../reference_2.md#object-fiscalyear) object for the passed date

**Deprecated**

---
## StaticMethod: Date.getLogicalDateOnly

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

**Deprecated**

---
## StaticMethod: Date.getLogicalTimeOnly

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

**Deprecated**

---
## StaticMethod: Date.createLogicalDate

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

**Deprecated**

---
## StaticMethod: Date.compareDates

### Description
Compare two dates; returns 0 if equal, -1 if the first date is greater (later), or 1 if the second date is greater. If either value is not a Date object, it is treated as the epoch (midnight on Jan 1 1970) for comparison purposes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date1 | [Date](#type-date) | false | — | first date to compare |
| date2 | [Date](#type-date) | false | — | second date to compare |

### Returns

`[int](../reference.md#type-int)` — 0 if equal, -1 if first date > second date, 1 if second date > first date

**Deprecated**

---
## StaticMethod: Date.getDayNames

### Description
Return an array of the full names of each day, suitable for use in a selection list, etc. Day names are picked up from [DateUtil.dayNames](DateUtil.md#classattr-dateutildaynames), which defaults to an array of English-language strings and these are updated to localized values by loading a locale.

If `DateUtil.dayNames` is purposely cleared, this method will fall back to deriving day-names from the native browser date string. Note, if we have to use this native backup behavior, the day names may vary by browser as well as locale - for example, they may be in an abbreviated form, similar to the result of calling [DateUtil.getShortDayNames](DateUtil.md#classmethod-dateutilgetshortdaynames).

### Returns

`[Array of String](#type-array-of-string)` — array of day names

### Groups

- dateFormatting

**Deprecated**

---
## StaticMethod: Date.parseInput

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

**Deprecated**

---
## StaticMethod: Date.setShowChooserWeekPickers

### Description
Sets the global attribute that dictates whether the [choosers](DateChooser.md#class-datechooser) shelled from [DateItems](DateItem.md#class-dateitem) show a UI for working with Weeks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showChooserWeekPickers | [boolean](../reference.md#type-boolean) | false | — | whether to show Fiscal Week pickers in DateChoosers by default |

**Deprecated**

---
## StaticMethod: Date.setShowChooserFiscalYearPickers

### Description
Sets the global attribute that dictates whether the [choosers](DateChooser.md#class-datechooser) shelled from [DateItems](DateItem.md#class-dateitem) show a UI for working with Fiscal Years.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showChooserFiscalYearPickers | [boolean](../reference.md#type-boolean) | false | — | whether to show Fiscal Year pickers in DateChoosers by default |

**Deprecated**

---
## StaticMethod: Date.create

### Description
Create a new `Date` object - synonym for `new Date(arguments)`

### Returns

`[Date](#type-date)` — Date object

**Deprecated**

---
## StaticMethod: Date.createLogicalTime

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

**Deprecated**

---
## StaticMethod: Date.compareLogicalDates

### Description
Compare two dates, normalizing out the time elements so that only the date elements are considered; returns 0 if equal, -1 if the first date is greater (later), or 1 if the second date is greater.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date1 | [Date](#type-date) | false | — | first date to compare |
| date2 | [Date](#type-date) | false | — | second date to compare |

### Returns

`[int](../reference.md#type-int)` — 0 if equal, -1 if first date > second date, 1 if second date > first date. Returns false if either argument is not a date

**Deprecated**

---
## StaticMethod: Date.getFirstDayOfWeek

### Description
Returns the global attribute that dictates which day should be treated as the first day of the week in calendars and date calculations. The parameter is expected to be an integer value between 0 (Sunday) and 6 (Saturday).

The default value is picked up from the current locale.

### Returns

`[int](../reference.md#type-int)` — the number of the day being used as the first day of the week

**Deprecated**

---
## StaticMethod: Date.setDefaultDateSeparator

### Description
Sets a new default separator that will be used when formatting dates. By default, this is a forward slash character: "/"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| separator | [String](#type-string) | false | — | separator to use in dates |

### Groups

- dateFormatting

**Deprecated**

---
## StaticMethod: Date.getShortDayNames

### Description
Return an array of the short names of each day, suitable for use in a selection list, etc. Day names are picked up from a [DateUtil.shortDayNames](DateUtil.md#classattr-dateutilshortdaynames) list specified in each locale.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| length | [int](../reference.md#type-int) | false | — | maximum length of each day string - default is no maximum (full strings) |

### Returns

`[Array of String](#type-array-of-string)` — array of short day names

### Groups

- dateFormatting

**Deprecated**

---
## StaticMethod: Date.setWeekendDays

### Description
Sets the days that are considered [weekend days](DateUtil.md#classattr-dateutilweekenddays). The parameter should be array of the integers returned by the JavaScript built-in Date.getDay(), eg, 0 is Sunday and 6 is Saturday. Override to accommodate different workweeks such as Saudi Arabia (Saturday -> Wednesday) or Israel (Sunday -> Thursday).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| weekendDays | [Array of Integer](#type-array-of-integer) | false | — | the array of day-numbers to assign as weekend days |

**Deprecated**

---
## StaticMethod: Date.getFiscalStartDate

### Description
Returns the start date of the fiscal year for the passed date.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date)|[number](#type-number) | false | — | the date, or the year-number, to get the fiscal year for |
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the object representing the starts of one or more fiscal years |

### Returns

`[Date](#type-date)` — the start of the fiscal year for the passed date and fiscalCalendar

**Deprecated**

---
## StaticMethod: Date.getWeekendDays

### Description
Return an array of days that are considered "weekend" days. Values will be the integers returned by the JavaScript built-in Date.getDay(), eg, 0 is Sunday and 6 is Saturday. Override [DateUtil.weekendDays](DateUtil.md#classattr-dateutilweekenddays) to accommodate different workweeks such as Saudi Arabia (Saturday -> Wednesday) or Israel (Sunday -> Thursday).

### Returns

`[Array of Integer](#type-array-of-integer)` — array of weekend days

### Groups

- dateFormatting

**Deprecated**

---
## StaticMethod: Date.getInputFormat

### Description
Retrieves the default format for strings being parsed into dates via `DateUtil.parseInput()`

### Returns

`[String](#type-string)` — the current inputFormat for dates

### See Also

- [DateUtil.setInputFormat](DateUtil.md#classmethod-dateutilsetinputformat)

**Deprecated**

---
## StaticMethod: Date.getFiscalCalendar

### Description
Returns the global [FiscalCalendar object](../reference.md#object-fiscalcalendar) representing the start month and date of the fiscal year in the current locale.

### Returns

`[FiscalCalendar](#type-fiscalcalendar)` — the FiscalCalendar object

**Deprecated**

---
## StaticMethod: Date.getDefaultDateSeparator

### Description
gets the default date separator string

### Returns

`[String](#type-string)` — the default date separator

### Groups

- dateFormatting

**Deprecated**

---
