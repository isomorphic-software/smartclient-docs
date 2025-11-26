# FiscalCalendar Documentation

[← Back to API Index](../reference.md)

---

## Attr: FiscalCalendar.defaultMonth

### Description
The default zero-based month-number to use for calculating fiscal dates when no [fiscal years](#attr-fiscalcalendarfiscalyears) are provided. This value together with [FiscalCalendar.defaultDate](#attr-fiscalcalendardefaultdate) will be used as the start date for the fiscal years where no explicitly specified fiscalYear configuration is present.  
See also [FiscalCalendar.defaultYearMode](#attr-fiscalcalendardefaultyearmode).

**Flags**: IRW

---
## Attr: FiscalCalendar.fiscalYears

### Description
An array of [FiscalYear objects](../reference_2.md#object-fiscalyear) which each represent the start date of a single fiscal year.

**Flags**: IRW

---
## Attr: FiscalCalendar.defaultDate

### Description
The default one-based day-number in the [specified month](#attr-fiscalcalendardefaultmonth) to use for calculating fiscal dates when no [fiscal years](#attr-fiscalcalendarfiscalyears) are provided. This value together with [FiscalCalendar.defaultMonth](#attr-fiscalcalendardefaultmonth) will be used as the start date for the fiscal years where no explicitly specified fiscalYear configuration is present.  
See also [FiscalCalendar.defaultYearMode](#attr-fiscalcalendardefaultyearmode).

**Flags**: IRW

---
## Attr: FiscalCalendar.defaultYearMode

### Description
This attribute controls how the displayed fiscalYear value should be calculated for dates falling within a period not explicitly listed in the [fiscal years array](#attr-fiscalcalendarfiscalyears).

The [FiscalCalendar.defaultMonth](#attr-fiscalcalendardefaultmonth) and [FiscalCalendar.defaultDate](#attr-fiscalcalendardefaultdate) will be used to calculate the start of the fiscal year period. The defaultYearMode determines whether the reported fiscalYear for this period matches the year in which the period starts or the year in which it ends (so whether a fiscal year spanning dates within both 2020 and 2021 is reported as fiscalYear 2020 or 2021).

**Flags**: IRW

---
