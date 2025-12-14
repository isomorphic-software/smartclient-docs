# Time Documentation

[← Back to API Index](../reference.md)

---

## Class: Time

### Description
Helper methods and system-wide defaults for dealing with time values and time display formats.

This class includes utility methods for the creation and display of logical time values, as well as modifying the default display timezone for datetime type values. See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on working with dates, times and datetimes in SmartClient.

---
## ClassAttr: Time.displayFormat

### Description
Standard formatter to be used when converting a date to a time-string via [Time.toTime](#classmethod-timetotime)

**Flags**: RWA

---
## ClassAttr: Time.defaultMillisecondSeparator

### Description
The separator character to include before the milliseconds element when parsing and formatting Time strings.

### Groups

- i18nMessages

**Flags**: RWA

---
## ClassAttr: Time.use24HourTime

### Description
Indicate whether calls to [DateUtil.format](DateUtil.md#classmethod-dateutilformat) with no formatter show times in 24-hour format. This includes UI elements, such as [TimeItems](TimeItem.md#class-timeitem) and [Calendars](Calendar.md#class-calendar), when no formatters are provided.

**Flags**: RWA

---
## ClassAttr: Time.defaultTimeSeparator

### Description
The separator character to include between hours, minutes and seconds when parsing and formatting Time strings.

### Groups

- i18nMessages

**Flags**: RWA

---
## ClassAttr: Time.shortDisplayFormat

### Description
Standard formatter to be used when converting a date to a time-string via [Time.toShortTime](#classmethod-timetoshorttime)

**Flags**: RWA

---
## ClassAttr: Time.PMIndicator

### Description
String appended to times to indicate am (when not using 24 hour format).

### Groups

- i18nMessages

**Flags**: RWA

---
## ClassAttr: Time.adjustForDST

### Description
Determines whether datetime formatters should consider the effect of Daylight Saving Time when computing offsets from UTC. By default, this flag is set during framework initialization if SmartClient detects that it is running in a locale that is observing DST this year. If you do not want DST adjustments to be applied, set this flag to false.

Note that setting this flag to true will have no effect unless you are in a locale that is observing Daylight Saving Time for the date in question; this is because we rely on the browser for offset information, and browsers are only capable of returning local date and time information for the computer's current locale.

This setting will not have any impact on the display of fields specified as type "time" or "date" (logical dates and logical times) - only on datetime type values. See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for information on working with dates, times and datetimes in SmartClient.

**Flags**: RWA

---
## ClassAttr: Time.UTCHoursOffset

### Description
Hour offset from UTC to use when formatting ["datetime"](../reference_2.md#type-fieldtype) type fields for display to the user.

Has no effect on fields specified as logical date (`field.type = "date";`) and logical time (`field.type = "time"`) fields.

**Deprecated**

**Flags**: IRA

---
## ClassAttr: Time.AMIndicator

### Description
String appended to times to indicate am (when not using 24 hour format).

### Groups

- i18nMessages

**Flags**: RWA

---
## ClassMethod: Time.toShortTime

### Description
Given a date object, return the time associated with the date as a short string. If no formatter is passed, use the standard formatter set up via [Time.setShortDisplayFormat](#classmethod-timesetshortdisplayformat)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | Date to convert to a time string. |
| formatter | [TimeDisplayFormat](../reference.md#type-timedisplayformat)|[FormatString](../reference.md#type-formatstring)|[Function](#type-function) | true | — | Optional custom formatter to use. Will accept a function (which will be passed a pointer to the Date to format), a format string, or a string designating a standard formatter |
| logicalTime | [boolean](../reference.md#type-boolean) | true | — | Is the date passed in a representation of a logical time value such as a value from a `"time"` type field on a dataSource or a datetime value? For datetime values the formatted string will respect any custom [display timezone](#classmethod-timesetdefaultdisplaytimezone). If not explicitly specified, the date passed in will be assumed to be a datetime unless it was created explicitly as a time via [Time.createLogicalTime](#classmethod-timecreatelogicaltime) or similar APIs. |

### See Also

- [Time.toTime](#classmethod-timetotime)

---
## ClassMethod: Time.getDefaultDisplayTimezone

### Description
Returns the default display timezone set up by [Time.setDefaultDisplayTimezone](#classmethod-timesetdefaultdisplaytimezone). If no explicit timezone has been set this will return the browser locale timezone offset.

### Returns

`[String](#type-string)` — String of the format `+/-HH:MM`

---
## ClassMethod: Time.setNormalDisplayFormat

### Description
Sets the default format for strings returned by [Time.toTime](#classmethod-timetotime).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| formatter | [TimeDisplayFormat](../reference.md#type-timedisplayformat)|[FormatString](../reference.md#type-formatstring)|[Function](#type-function) | false | — | Optional custom formatter to use. Will accept a function (which will be passed a pointer to the Date to format), a format string, or a string designating a standard formatter |

---
## ClassMethod: Time.createDate

### Description
Creates a date object with the time set to the hours, minutes and seconds passed in. Unless the `UTCTime` parameter is passed in, parameters are assumed to specify the time in native local display time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hours | [number](#type-number) | true | — | Hours for the date (defaults to zero) |
| minutes | [number](#type-number) | true | — | Minutes for the date (defaults to zero) |
| seconds | [number](#type-number) | true | — | Seconds for the date (defaults to zero) |
| milliseconds | [number](#type-number) | true | — | Milliseconds for the date (defaults to zero) |
| UTCTime | [boolean](../reference.md#type-boolean) | true | — | If true, treat the time passed in as UTC time rather than local time |

**Deprecated**

---
## ClassMethod: Time.createLogicalTime

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
## ClassMethod: Time.setDefaultDisplayTimezone

### Description
Sets the offset from UTC to use when formatting values of type [datetime](../reference_2.md#type-fieldtype) with standard display formatters.

This property affects how dates are displayed and also the assumed timezone for user-input. For a concrete example - assume this method has been called and passed a value of "+01:00", and an application has a [DateTimeItem](DateTimeItem.md#class-datetimeitem) visible in a DynamicForm. If the value of this field is set to the current date, with UTC time set to "10:00", the time portion of the value displayed in the form item will be "11:00". Similarly if a user modifies the time value in the text box to be "16:00", a call to [FormItem.getValue](FormItem.md#method-formitemgetvalue) for the item will return a date object with UTC time set to 15:00.

Interaction with daylight savings time: The specified "defaultDisplayTimezone" should reflect the correct UTC offset for the current date, for which it will always be exactly respected; adjustment will only be made for dates that fall outside the current daylight savings time mode.

In other words if DST is currently not in effect (IE: the current date is a Winter date), any other dates where DST is not in effect will be formatted to exactly respect the specified defaultDisplayTimezone (so for defaultDisplayTimezone of "+01:00", the display string will be 1 hour ahead of the UTC time on the date in question), and any dates where DST is in effect would be further adjusted to account for DST (so the display string would be 2 hours ahead for dates that fall in the Summer).  
Alternatively if DST currently is in effect (EG: Current date is a Summer date) the situation is reversed. Any date value for which DST should be applied will be be formatted for display with an offset of 1 hour from UTC - and any date value for which DST should not be applied would be formatted with an offset of 0 hours from UTC.  
Note that the [Time.adjustForDST](#classattr-timeadjustfordst) property may be set to `false` to disable this logic - in this case the time portion of dates will always be offset from UTC by exactly the specified defaultDisplayOffset, regardless of whether they fall in the range where Daylight Savings Time would usually be applied or not.

Note that if a custom timezone is specified, it will not effect native javascript date formatting functions such as `toLocaleString()`. See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more on how SmartClient handles date and time formatting and storage.

If this method is never called, the default display timezone for times and datetimes will be derived from the native browser local timezone.

Note that the displayTimezone effects datetime fields only and has no effect on fields specified as logical date (`field.type = "date";`) or logical time (`field.type = "time"`).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| offset | [String](#type-string) | false | — | offset from UTC. This should be a string in the format `+/-HH:MM` for example `"-08:00"` |

### See Also

- [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage)

---
## ClassMethod: Time.toTime

### Description
Given a date object, return the time associated with the date as a formatted string. If no formatter is passed, use the standard formatter set up via [Time.setNormalDisplayFormat](#classmethod-timesetnormaldisplayformat).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| date | [Date](#type-date) | false | — | Date to convert to a time string. |
| formatter | [TimeDisplayFormat](../reference.md#type-timedisplayformat)|[FormatString](../reference.md#type-formatstring)|[Function](#type-function) | true | — | Optional custom formatter to use. Will accept a function (which will be passed a pointer to the Date to format), a format string, or a string designating a standard formatter |
| logicalTime | [boolean](../reference.md#type-boolean) | true | — | Is the date passed in a representation of a logical time value such as a value from a `"time"` type field on a dataSource or a datetime value? For datetime values the formatted string will respect any custom [display timezone](#classmethod-timesetdefaultdisplaytimezone). If not explicitly specified, the date passed in will be assumed to be a datetime unless it was created explicitly as a time via [Time.createLogicalTime](#classmethod-timecreatelogicaltime) or similar APIs. |

### See Also

- [Time.toShortTime](#classmethod-timetoshorttime)

---
## ClassMethod: Time.setShortDisplayFormat

### Description
Sets the default format for strings returned by [Time.toShortTime](#classmethod-timetoshorttime).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| formatter | [TimeDisplayFormat](../reference.md#type-timedisplayformat)|[FormatString](../reference.md#type-formatstring)|[Function](#type-function) | false | — | Optional custom formatter to use. Will accept a function (which will be passed a pointer to the Date to format), a format string, or a string designating a standard formatter |

---
## ClassMethod: Time.compareTimes

### Description
Compares the times of 2 dates, or strings. If a string is passed as one of the parameters it should be in a format that converts to a valid time such as `"1:30pm"`, `"13:30"`, or `"1:30:45pm"`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| time1 | [Date](#type-date)|[String](#type-string) | false | — | First time to compare |
| time2 | [Date](#type-date)|[String](#type-string) | false | — | Second time to compare |

### Returns

`[boolean](../reference.md#type-boolean)` — True if the times match, false if not

---
## ClassMethod: Time.parseInput

### Description
Converts a time-string such as `1:00pm` to a new Date object representing a logical time value (rather than a specific datetime value), typically for display in a [time type field](DataSourceField.md#attr-datasourcefieldtype). Accepts most formats of time string. The generated Date value will have year, month and date set to the epoch date (Jan 1 1970), and time elements set to the supplied hour, minute and second (in browser native local time).

See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on date, time and datetime values in SmartClient.

It may be a common hack for a server framework (e.g. aspx) where there is no "time of day" type - only a full DateTime, or a TimeSpan - to return a string in [ISO 8601 duration format](https://en.wikipedia.org/wiki/ISO_8601) for field values with type Time in the DataSource definition. We recognize and parse that format here, but if you have the ability to change the type, the best approach would probably be to switch the type to one fully supported server-side, such as DateTime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| timeString | [String](#type-string) | false | — | time string to convert to a date |
| validTime | [boolean](../reference.md#type-boolean) | false | — | If this method is passed a timeString in an unrecognized format, return null rather than a date object with time set to 00:00:00 |

---
