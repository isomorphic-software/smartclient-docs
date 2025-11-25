# TextExportSettings Documentation

[← Back to API Index](../main.md)

---

## Class: TextExportSettings

*Inherits from:* [TextSettings](TextSettings.md#class-textsettings)

### Description
Settings for use with [DataSource.recordsAsText](DataSource.md#method-datasourcerecordsastext).

---
## Attr: TextExportSettings.lineSeparator

### Description
Separator between Records. Default is a newline character ("\\n").

**Flags**: IR

---
## Attr: TextExportSettings.quoteValues

### Description
Whether to surround each value with quotes ("").

**Flags**: IR

---
## Attr: TextExportSettings.timeFormat

### Description
Format to use when outputting time values. Default is 24 hour time.

**Flags**: IR

---
## Attr: TextExportSettings.useDisplayValue

### Description
Whether to convert each field's value to the corresponding display value for export. Default of false will directly export the field's value.

**Flags**: IR

---
## Attr: TextExportSettings.forceText

### Description
If set, all text fields will use the indicated [ForceTextApproach](../main.md#type-forcetextapproach) unless they have a specific setting for [DataSourceField.exportForceText](DataSourceField.md#attr-datasourcefieldexportforcetext).

**Flags**: IR

---
## Attr: TextExportSettings.dateTimeFormat

### Description
Format to use when outputting datetime values. Default is to combine the configured date and time formats with a space (" ").

**Flags**: IR

---
## Attr: TextExportSettings.nullValueText

### Description
Text to export for a field with a null value. If this property is null, then null fields will be assumed to have the default value for their field type.

**Flags**: IR

---
## Attr: TextExportSettings.dateFormat

### Description
Format to use when outputting date values. Default is to use the format expected by Microsoft Excel (eg 1-2-2011), which Excel will turn into a real date value (see [excelPasting](../kb_topics/excelPasting.md#kb-topic-copy-and-paste-with-excel)). The current month-day-year order as set by [DateUtil.setInputFormat](DateUtil.md#classmethod-dateutilsetinputformat) will be used.

**Flags**: IR

---
