# dsSpecialFields

[← Back to API Index](../reference.md)

---

## KB Topic: dsSpecialFields

### Description
A DataSource allows you to declare that certain fields are the most important fields to show to a user in situations where space is limited, and only one or a few fields can be reasonably shown.

In the table below these special fields are summarized, along with their meaning, and examples of which field would be most appropriate from several example DataSources.

| Attribute | Example DataSource field | Meaning |
|---|---|---|
| employee | emailMessage | stockItem |
| titleField | name | subject | itemName | primary label for the record as a while |
| infoField | job | sender | category | second most pertinent piece of textual information |
| dataField | salary | date | price | most pertinent numeric, date or enum (eg status) field |
| descriptionField | bio | messageBody | description | descriptive long text field |
| iconField | photo | statusIcon | thumbnail | an image or icon to accompany the title field |

Examples of the use of these fields include the [TileGrid](../classes/TileGrid.md#class-tilegrid)'s default choice of fields, and the [drag tracker](../classes/EventHandler.md#classmethod-eventhandlersetdragtracker) that follows the mouse cursor when data is being dragged between grids.

### Related

- [DataSource.titleField](../classes/DataSource.md#attr-datasourcetitlefield)
- [DataSource.iconField](../classes/DataSource.md#attr-datasourceiconfield)
- [DataSource.infoField](../classes/DataSource.md#attr-datasourceinfofield)
- [DataSource.dataField](../classes/DataSource.md#attr-datasourcedatafield)
- [DataSource.descriptionField](../classes/DataSource.md#attr-datasourcedescriptionfield)

---
