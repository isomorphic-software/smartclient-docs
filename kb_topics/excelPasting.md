# Copy and Paste with Excel

[← Back to API Index](../main.md)

---

## KB Topic: Copy and Paste with Excel

### Description
[DataSource.recordsAsText](../classes/DataSource.md#method-datasourcerecordsastext) can export a set of DataSource records in tab-separated-values format so that it can be copied and pasted into a Microsoft Excel spreadsheet.

However, be aware that Excel does a bunch of type guessing on pasted data:

*   values that look like dates (eg 1-2-2011 and even just 1-2) will become true date-valued cells (as indicated by Excel rendering them as eg 2-Jan). Note that the month-day-year interpretation is **locale-dependent** so be sure text is exported
*   values that look numeric, eg "5.0" become true number values (as indicated by Excel showing just "5")
*   values that look like times, eg "5:30", will be converted to times (as indicated by Excel showing 5:30:00 AM when editing the value)
*   values with a leading "=" will be treated as formulas

Unfortunately, when these behaviors are undesirable, there is no means of turning them off that doesn't have any drawbacks. You can:

*   adding a leading space or other char (but this changes the cell value).
*   turning the cell into a trivial formula, eg ="literal value". But this means that when the cell is edited, it's value is a formula.
*   format the cells as text in Excel before pasting data onto them

The first or second approach can be enabled when exporting text - see [DataSource.recordsAsText](../classes/DataSource.md#method-datasourcerecordsastext) and [DataSourceField.exportForceText](../classes/DataSourceField.md#attr-datasourcefieldexportforcetext).

---
