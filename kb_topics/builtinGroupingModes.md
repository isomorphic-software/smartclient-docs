# Built-in Grouping Modes

[← Back to API Index](../reference.md)

---

## KB Topic: Built-in Grouping Modes

### Description
[SimpleTypes](../classes/SimpleType.md#class-simpletype) support a mechanism for arranging values into groups.

These [Grouping modes](../classes/SimpleType.md#attr-simpletypegroupingmodes) can be applied to any SimpleType, but some types already support a set of builtin modes, as follows:

**Date Grouping modes**

*   day/dayOfWeek: Group by week-day, all weeks
*   dayOfMonth: Group by month-day, all months
*   week: Group by Week number, all years
*   month: Group by Month number, all years
*   quarter: Group by Quarter, all years
*   year: Group by Year
*   upcoming: Various specific date groups: Today, Yesterday, Last Week, Last Month, etc
*   date: Group by specific Date
*   dayOfWeekAndYear: Group by week-day, week and year
*   dayOfMonthAndYear: Group by month-day, month and year
*   weekAndYear: Group by week-number and year
*   monthAndYear: Group by month and year
*   quarterAndYear: Group by quarter and year

**Time Grouping modes**

*   hours: Group by hours value
*   minutes: Group by minutes value
*   seconds: Group by seconds value
*   milliseconds: Group by milliseconds value

---
