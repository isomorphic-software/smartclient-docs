# TextSettings Documentation

[← Back to API Index](../reference.md)

---

## Class: TextSettings

### Description
Common base class of [TextImportSettings](TextImportSettings.md#class-textimportsettings).

---
## Attr: TextSettings.fieldList

### Description
For export, a set of fields to export. Default is to export all DataSource fields.

Fields may be specified that are not in the DataSource but for which data values are present in the provided Records. In this case the field is assumed to be of type "text".

For import, names of DataSource fields to use to parse values, in order.

If `fieldList` is unset, DataSource fields are used, in order.

If more values exist in a given Record than the listed fields or than all DataSource fields, remaining values are ignored.

**Flags**: IR

---
## Attr: TextSettings.lineSeparator

### Description
Separator between Records. For import, default of null means that either the Unix/Mac format of just a newline ("\\n") or the typical DOS/Windows format of a carriage return and newline ("\\r\\n") will be accepted. For export, overridden in [TextExportSettings](TextExportSettings.md#class-textexportsettings).

**Flags**: IR

---
## Attr: TextSettings.escapingMode

### Description
[EscapingMode](../reference.md#type-escapingmode) expected for escaping special characters embedded in text values.

**Flags**: IR

---
## Attr: TextSettings.fieldSeparator

### Description
Separator between field values. Default is a comma character, producing CSV (comma-separated values) format.

**Flags**: IR

---
