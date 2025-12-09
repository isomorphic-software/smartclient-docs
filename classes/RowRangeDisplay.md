# RowRangeDisplay Documentation

[← Back to API Index](../reference.md)

---

## Class: RowRangeDisplay

*Inherits from:* [Label](Label.md#class-label)

### Description
Specialized [Label](Label.md#class-label) for showing the currently visible row range and row count for a source listGrid.

A rowRangeDisplay may be requested directly from the source grid via [ListGrid.getRowRangeDisplay](ListGrid_2.md#method-listgridgetrowrangedisplay).

### Groups

- rowRangeDisplay

---
## Attr: RowRangeDisplay.canRequestRowCount

### Description
When an exact row count is currently unavailable on the source listGrid's [data object](ResultSet.md#method-resultsetgetrowcountstatus), can the user issue a [row count fetch](ResultSet.md#method-resultsetfetchrowcount) by clicking?

For a rowRangeDisplay created via [ListGrid.getRowRangeDisplay](ListGrid_2.md#method-listgridgetrowrangedisplay) this value will be set to [ListGrid.canRequestRowCount](ListGrid_1.md#attr-listgridcanrequestrowcount)

See also [RowRangeDisplay.interactiveStyleName](#attr-rowrangedisplayinteractivestylename) and [RowRangeDisplay.requestRowCountPrompt](#attr-rowrangedisplayrequestrowcountprompt).

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: RowRangeDisplay.sourceGrid

### Description
The [ListGrid](ListGrid_1.md#class-listgrid) for which this label displays the current row range and row count.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: RowRangeDisplay.align

### Description
rowRangeDisplay will center its content by default.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: RowRangeDisplay.interactiveStyleName

### Description
If [RowRangeDisplay.canRequestRowCount](#attr-rowrangedisplaycanrequestrowcount) is true, this style name will be applied to the rowRangeDisplay as long as an accurate row count is not known, indicating to the user that they may click the label to retrieve an accurate status value.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: RowRangeDisplay.vlign

### Description
rowRangeDisplay will vertically center its content by default.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: RowRangeDisplay.wrap

### Description
rowRangeDisplay will not allow its content to wrap by default

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: RowRangeDisplay.requestRowCountPrompt

### Description
This prompt will be displayed in a hover when [RowRangeDisplay.canRequestRowCount](#attr-rowrangedisplaycanrequestrowcount) is true and an accurate row count is not currently known. This indicates to the user that they can click to issue a [row count fetch](ListGrid_2.md#method-listgridfetchrowcount) request.

If set to null, no hover prompt will be displayed by default

### Groups

- i18nMessages

**Flags**: IRW

---
## Method: RowRangeDisplay.setSourceGrid

### Description
Setter for the [RowRangeDisplay.sourceGrid](#attr-rowrangedisplaysourcegrid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sourceGrid | [ListGrid](#type-listgrid) | false | — | ListGrid to display row information about |

### Groups

- rowRangeDisplay

---
