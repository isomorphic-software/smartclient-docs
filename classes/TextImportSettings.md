# TextImportSettings Documentation

[← Back to API Index](../main.md)

---

## Class: TextImportSettings

*Inherits from:* [TextSettings](TextSettings.md#class-textsettings)

### Description
Settings for use with [DataSource.recordsFromText](DataSource.md#method-datasourcerecordsfromtext).

---
## Attr: TextImportSettings.hasHeaderLine

### Description
If set to true, the data is assumed to have a header line that lists titles for each field, which should be parsed.

`recordsFromText` will then try to find a same-named DataSourceField by checking parsed titles against both [DataSourceField.title](DataSourceField.md#attr-datasourcefieldtitle) and [DataSourceField.name](DataSourceField.md#attr-datasourcefieldname) (titles first), doing a case-insensitive comparison with any leading or trailing whitespace removed from the title. If no field matches, data will appear in the returned Records under the exact title parsed from the header line.

If this approach will not find appropriate DataSourceFields, parse the header line before calling `recordsFromText()`, and provide the list of field names to use when parsing data as [TextSettings.fieldList](TextSettings.md#attr-textsettingsfieldlist).

**Flags**: IR

---
