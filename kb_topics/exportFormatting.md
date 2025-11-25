# Exports & Formatting

[← Back to API Index](../main.md)

---

## KB Topic: Exports & Formatting

### Description
This topic explains the default rules for whether date, numeric and other formatting settings are applied when performing various types of exports, and how to override the default behavior.

For server-based exports (e.g. [ListGrid.exportData](../classes/ListGrid_2.md#method-listgridexportdata) or [DataSource.exportData](../classes/DataSource.md#method-datasourceexportdata)):

*   if [exportAs](../classes/DSRequest.md#attr-dsrequestexportas) is a spreadsheet format (XLS or OOXML), [dsField.format](../classes/DataSourceField.md#attr-datasourcefieldformat) or [dsField.exportFormat](../classes/DataSourceField.md#attr-datasourcefieldexportformat) will be used if specified, otherwise, [DataSourceField.dateFormatter](../classes/DataSourceField.md#attr-datasourcefielddateformatter) will be used if specified, otherwise, no formatting will be applied and the date or number will be shown in the spreadsheet program's default formatting.
*   if targetting CSV, XML or JSON, by default, formatting declarations are ignored and standard formats are used, because the expectation is that this type of export is intended for data interchange with other systems and not for direct viewing by end users. Specifically, date and datetime values use standard [XML Schema date and time formats](http://www.w3.org/TR/xmlschema-2/#dateTime) and CSV export uses the "yyyy-MM-dd HH:mm:ss" expected by Microsoft Excel and similar tools that consume CSV, with only the date or time part of the format being used for fields that are of type "date" or "time" rather than "datetime". If you instead set [DSRequest.exportRawValues](../classes/DSRequest.md#attr-dsrequestexportrawvalues) to false, format settings available to server will be used, exactly as explained above for spreadsheet exports with `exportData()`.

For a client-driven export (e.g. [ListGrid.exportClientData](../classes/ListGrid_2.md#method-listgridexportclientdata) or [DataSource.exportClientData](../classes/DataSource.md#method-datasourceexportclientdata):

*   if [exportAs](../classes/DSRequest.md#attr-dsrequestexportas) is a spreadsheet format (XLS or OOXML), rules are the same as for server-driven export, except that if no [dsField.format](../classes/DataSourceField.md#attr-datasourcefieldformat) or [dsField.exportFormat](../classes/DataSourceField.md#attr-datasourcefieldexportformat) is specified, `dateFormatter` settings on client-side UI components will be used if a built-in formatter is used (for example, if [ListGridField.dateFormatter](../classes/ListGridField.md#attr-listgridfielddateformatter) is set to the built-in formatter "toEuropeanShortDate"). If you need date or number values to appear **exactly** as shown to the user, set [DSRequest.exportDatesAsFormattedString](../classes/DSRequest.md#attr-dsrequestexportdatesasformattedstring) or [DSRequest.exportNumbersAsFormattedString](../classes/DSRequest.md#attr-dsrequestexportnumbersasformattedstring), respectively, but see the docs for these properties for the drawbacks of doing this.
*   for CSV, XML or JSON exports, whatever is shown to the end user is used (since it's assumed the reason for calling `exportClientData()` rather than `exportData()` is precisely to create a fully formatted export). If you instead set [ListGrid.exportRawValues](../classes/ListGrid_1.md#attr-listgridexportrawvalues) to true, only standard formats appropriate to data interchange are used, the same as described for `exportData()` above.

These different default behaviors for different export formats can be overriden by use of [ListGrid.exportRawValues](../classes/ListGrid_1.md#attr-listgridexportrawvalues). If you only want to override the default behaviors for numeric values, you can use [ListGrid.exportRawNumbers](../classes/ListGrid_1.md#attr-listgridexportrawnumbers) (note, the `exportRawNumbers` setting has no effect if `exportRawValues` is set to true)

Use [DSRequest.exportPropertyIdentifier](../classes/DSRequest.md#attr-dsrequestexportpropertyidentifier) to override the default behavior for a server or client-driven export and force either component field names or titles to be exported.

#### Display-mapped fields
SmartClient supports a number of ways to declaratively map underlying data values to "display values" that have more meaning to a user. This mapping can be achieved using a [displayField](../classes/DataSourceField.md#attr-datasourcefielddisplayfield) in the same record, a [ValueMap](../main_2.md#type-valuemap) or an [optionDataSource](../classes/ListGridField.md#attr-listgridfieldoptiondatasource). The table below shows what values get exported for each of these possibilities, in combination with the [exportValueFields](../classes/DSRequest.md#attr-dsrequestexportvaluefields) flag and whether you are using client-driven or server-driven export:

| Use case | Exports value field | Exports display field |
|---|---|---|
| exportClientData(), in-record displayField, exportValueFields=true | ✓ | ✓ |
| exportClientData(), in-record displayField, exportValueFields=false |  | ✓ |
| exportClientData(), valueMap declared in DataSource, exportValueFields=true |  | ✓ |
| exportClientData(), valueMap declared in DataSource, exportValueFields=false |  | ✓ |
| exportClientData(), valueMap defined in code, exportValueFields=true |  | ✓ |
| exportClientData(), valueMap defined in code, exportValueFields=false |  | ✓ |
| exportClientData(), optionDataSource, exportValueFields=true | ✓ | ✓ |
| exportClientData(), optionDataSource, exportValueFields=false |  | ✓ |
| exportData(), in-record displayField (must be declared in DataSource), exportValueFields not specified | ✓ | ✓ |
| exportData(), in-record displayField (must be declared in DataSource), exportValueFields=true | ✓ |  |
| exportData(), in-record displayField (must be declared in DataSource), exportValueFields=false |  | ✓ |
| exportData(), valueMap declared in DataSource | ✓ |  |
| exportData(), valueMap defined in code | ✓ |  |
| exportData(), optionDataSource | ✓ |  |

### Related

- [CubeGrid.valueFormat](../classes/CubeGrid.md#attr-cubegridvalueformat)
- [CubeGrid.valueExportFormat](../classes/CubeGrid.md#attr-cubegridvalueexportformat)
- [DetailViewerField.format](../classes/DetailViewerField.md#attr-detailviewerfieldformat)
- [DetailViewerField.exportFormat](../classes/DetailViewerField.md#attr-detailviewerfieldexportformat)
- [ListGridField.format](../classes/ListGridField.md#attr-listgridfieldformat)
- [ListGridField.exportFormat](../classes/ListGridField.md#attr-listgridfieldexportformat)
- [SimpleType.format](../classes/SimpleType.md#attr-simpletypeformat)
- [SimpleType.exportFormat](../classes/SimpleType.md#attr-simpletypeexportformat)
- [DSRequest.exportRawValues](../classes/DSRequest.md#attr-dsrequestexportrawvalues)
- [DSRequest.exportPropertyIdentifier](../classes/DSRequest.md#attr-dsrequestexportpropertyidentifier)
- [DSRequest.exportDatesAsFormattedString](../classes/DSRequest.md#attr-dsrequestexportdatesasformattedstring)
- [DSRequest.exportNumbersAsFormattedString](../classes/DSRequest.md#attr-dsrequestexportnumbersasformattedstring)
- [DSRequest.exportTZ](../classes/DSRequest.md#attr-dsrequestexporttz)
- [FormItem.exportFormat](../classes/FormItem.md#attr-formitemexportformat)

---
