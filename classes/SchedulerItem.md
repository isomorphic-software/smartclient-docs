# SchedulerItem Documentation

[← Back to API Index](../reference.md)

---

## Class: SchedulerItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
A self-contained cadence editor for [scheduled report delivery](../kb_topics/scheduledDelivery.md#kb-topic-report-delivery-and-scheduling). Presents a compact form with frequency (Daily/Weekly/Monthly), a day-of-week picker for Weekly and a day-of-month picker for Monthly (each shown only for its frequency via declarative `visibleWhen`), a send time in [SchedulerItem.minuteIncrement](#attr-scheduleritemminuteincrement) steps, and a time zone.

[SchedulerItem.getScheduleValue](#method-scheduleritemgetschedulevalue) returns the resolved schedule configuration including a 5-field Unix cron expression. [SchedulerItem.describeSchedule](#method-scheduleritemdescribeschedule) produces a human-readable phrase (e.g. "daily at 9:00 AM EST") suitable for confirmation messages.

The item is storage-agnostic: it computes cadence values but has no dependency on the schedule DataSource, the server DMI, or Quartz. A host form receives edit notifications via [SchedulerItem.scheduleChanged](#method-scheduleritemschedulechanged).

### Groups

- scheduledDelivery

---
## Attr: SchedulerItem.maxDayOfMonth

### Description
Last day offered for a Monthly schedule. The default, 28, is a day every month has, so a Monthly schedule never skips a month.

### Groups

- scheduledDelivery

**Flags**: IR

---
## Attr: SchedulerItem.timeZones

### Description
The time zones offered: a map of IANA time-zone id to a "Location (Zone Name)" label. The generic zone name ("Eastern Time") avoids the seasonal EST/EDT ambiguity, while the stored IANA id keeps the schedule correct across daylight-saving changes. The default covers the major world zones; set this to offer a different set (a report's Schedule dialog takes it from [DataReport.scheduleTimeZones](DataReport.md#attr-datareportscheduletimezones)). [SchedulerItem.describeSchedule](#method-scheduleritemdescribeschedule) shows the label, not the id.

### Groups

- scheduledDelivery

**Flags**: IR

---
## Attr: SchedulerItem.minuteIncrement

### Description
Step between the minutes offered for the send time. Any hour can be chosen.

### Groups

- scheduledDelivery

**Flags**: IR

---
## ClassMethod: SchedulerItem.describeCron

### Description
Returns a human-readable phrase for a 5-field Unix cron expression of the kind this item produces, e.g. "every weekday at 8:00 AM, New York (Eastern Time)" or "on the 15th of every month at 6:30 PM, London (UK Time)". Used for an item's [SchedulerItem.describeSchedule](#method-scheduleritemdescribeschedule) and to describe stored schedules, so both read the same. Expressions this item cannot produce are returned as they are.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cronExpression | [String](#type-string) | false | — | 5-field Unix cron (MIN HOUR DOM MONTH DOW) |
| timezone | [String](#type-string) | true | — | IANA time-zone id the expression is read in |
| timeZones | [Object](../reference_2.md#type-object) | true | — | map of time-zone id to display label; defaults to [SchedulerItem.timeZones](#attr-scheduleritemtimezones) |

### Returns

`[String](#type-string)` — cadence description

### Groups

- scheduledDelivery

---
## Method: SchedulerItem.describeSchedule

### Description
Returns a human-readable phrase describing the current cadence, e.g. "every weekday at 8:00 AM, New York (Eastern Time)". Suitable for confirmation messages and summary labels.

### Returns

`[String](#type-string)` — cadence description

### Groups

- scheduledDelivery

---
## Method: SchedulerItem.scheduleChanged

### Description
Notification fired whenever the user changes any cadence field (frequency, day, time, or time zone). Override or observe to update a live summary.

### Groups

- scheduledDelivery

---
## Method: SchedulerItem.setScheduleValue

### Description
Pre-populates the editor from an existing schedule. Accepts either the [SchedulerItem.getScheduleValue](#method-scheduleritemgetschedulevalue) shape or a server record with a `cronExpression` field. When a `cronExpression` is provided, the best-matching base frequency is inferred and time/days are parsed from the cron fields.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cfg | [Object](../reference_2.md#type-object) | false | — | schedule configuration |

### Groups

- scheduledDelivery

---
## Method: SchedulerItem.getScheduleValue

### Description
Returns the resolved schedule configuration as an object with the following properties:

*   `cronExpression` -- resolved 5-field Unix cron (MIN HOUR DOM MONTH DOW), the wire format sent to the server
*   `frequency` -- display name ("Daily", "Weekly", "Monthly")
*   `daysOfWeek` -- array of day abbreviations for Weekly, else null
*   `dayOfMonth` -- day of the month (1 to [SchedulerItem.maxDayOfMonth](#attr-scheduleritemmaxdayofmonth)) for Monthly, else null
*   `time` -- send time as "HH:MM AM/PM"
*   `timezone` -- IANA time-zone id (e.g. "America/New\_York")

### Returns

`[Object](../reference_2.md#type-object)` — schedule configuration

### Groups

- scheduledDelivery

---
