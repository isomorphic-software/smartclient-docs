# TableView Documentation

[← Back to API Index](../main.md)

---

## Class: TableView

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
Shows a listing of records with one or more fields from each record, with built-in support for navigation and editing of lists of records.

The TableView provides built-in controls such as [navigation arrows](#attr-tableviewshownavigation) and shows fields from the provided records in one of several built-in [RecordLayout](../main_2.md#type-recordlayout)s.

NOTE: This widget is intended primarily for creating handset/phone-sized interfaces and does not have an appearance in any skin other than Mobile.

---
## ClassAttr: TableView.WHOLE_RECORD

### Description
A declared value of the enum type [NavigationMode](../main.md#type-navigationmode).

**Flags**: R

---
## ClassAttr: TableView.SUMMARY_DATA

### Description
A declared value of the enum type [RecordLayout](../main_2.md#type-recordlayout).

**Flags**: R

---
## ClassAttr: TableView.TITLE_DESCRIPTION

### Description
A declared value of the enum type [RecordLayout](../main_2.md#type-recordlayout).

**Flags**: R

---
## ClassAttr: TableView.GROUPED

### Description
A declared value of the enum type [TableMode](../main.md#type-tablemode).

**Flags**: R

---
## ClassAttr: TableView.SUMMARY_INFO

### Description
A declared value of the enum type [RecordLayout](../main_2.md#type-recordlayout).

**Flags**: R

---
## ClassAttr: TableView.TITLE_ONLY

### Description
A declared value of the enum type [RecordLayout](../main_2.md#type-recordlayout).

**Flags**: R

---
## ClassAttr: TableView.PLAIN

### Description
A declared value of the enum type [TableMode](../main.md#type-tablemode).

**Flags**: R

---
## ClassAttr: TableView.NAVICON_ONLY

### Description
A declared value of the enum type [NavigationMode](../main.md#type-navigationmode).

**Flags**: R

---
## ClassAttr: TableView.SUMMARY_FULL

### Description
A declared value of the enum type [RecordLayout](../main_2.md#type-recordlayout).

**Flags**: R

---
## Attr: TableView.infoField

### Description
Field to display as part of individual record in "summary" [RecordLayout](../main_2.md#type-recordlayout)s.

### See Also

- [RecordLayout](../main_2.md#type-recordlayout)

**Flags**: IRW

---
## Attr: TableView.navIcon

### Description
The navigation icon shown next to records when [TableView.showNavigation](#attr-tableviewshownavigation) is true and [NavigationMode](../main.md#type-navigationmode) is set to "navIconOny".

**Flags**: IRW

---
## Attr: TableView.canSaveSearches

### Description
Option to save searches is disabled for TableView

**Flags**: IRA

---
## Attr: TableView.recordLayout

### Description
Sets the arrangement of data fields from the record.

Note that controls supported by the TableView itself, such as navigation icons, are implicitly added to the data fields described in the RecordLayout. If an [TableView.iconField](#attr-tableviewiconfield) has been configured, it too is an implicitly shown field, to the left of the area controlled by RecordLayout.

**Flags**: IRW

---
## Attr: TableView.descriptionField

### Description
Field to display as part of individual record in all [RecordLayout](../main_2.md#type-recordlayout)s except "titleOnly".

**Flags**: IRW

---
## Attr: TableView.titleField

### Description
Field to display for an individual record as the main title.

**Flags**: IRW

---
## Attr: TableView.navigationMode

### Description
Set navigation mode for this TableView.

**Flags**: IRW

---
## Attr: TableView.showNavigation

### Description
Whether to show navigation controls by default on all records. Can also be configured per-record with [TableView.recordNavigationProperty](#attr-tableviewrecordnavigationproperty).

**Flags**: IRW

---
## Attr: TableView.showIconField

### Description
Should an icon field be shown for each record? A column in the table is set aside for an icon as specified on each record in the [TableView.iconField](#attr-tableviewiconfield).

**Flags**: IRW

---
## Attr: TableView.wholeRecordNavIcon

### Description
The navigation icon shown next to records when [TableView.showNavigation](#attr-tableviewshownavigation) is true and [NavigationMode](../main.md#type-navigationmode) is set to "wholeRecord".

**Flags**: IRW

---
## Attr: TableView.recordNavigationProperty

### Description
Boolean property on each record that controls whether navigation controls are shown for that record. If property is not defined on the record a navigation icon is shown if [TableView.showNavigation](#attr-tableviewshownavigation) is `true`.

**Flags**: IRW

---
## Attr: TableView.recordTitleStyle

### Description
Default style for title.

**Flags**: IRW

---
## Attr: TableView.canShowFilterEditor

### Description
Option to show filter editor is disabled for TableView

**Flags**: IRA

---
## Attr: TableView.recordDescriptionStyle

### Description
Default style for description.

**Flags**: IRW

---
## Attr: TableView.recordInfoStyle

### Description
Default style for info field.

**Flags**: IRW

---
## Attr: TableView.dataField

### Description
Field to display as part of individual record in "summary" [RecordLayout](../main_2.md#type-recordlayout)s.

**Flags**: IRW

---
## Attr: TableView.recordDataStyle

### Description
Default style for data field.

**Flags**: IRW

---
## Attr: TableView.iconField

### Description
This property allows the developer to specify the icon displayed next to a record. Set `record[tableView.iconField]` to the URL of the desired icon to display. Only applies if [TableView.showIconField](#attr-tableviewshowiconfield) is `true`.

**Flags**: IRW

---
## Attr: TableView.tableMode

### Description
The display mode of the table.

**Flags**: IRW

---
## Method: TableView.formatRecord

### Description
Formatter to apply to record display.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to format |

### Returns

`[HTMLString](../main.md#type-htmlstring)` — formatted record contents

---
## Method: TableView.imageClick

### Description
Executed when the user clicks on the image displayed in a record if [TableView.iconField](#attr-tableviewiconfield) has been specified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record clicked |

---
## Method: TableView.recordNavigationClick

### Description
Executed when the user clicks on a record, or on the navigate icon for a record depending on [NavigationMode](../main.md#type-navigationmode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record clicked |

---
