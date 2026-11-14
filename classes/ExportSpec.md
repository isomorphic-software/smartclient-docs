# ExportSpec Documentation

[← Back to API Index](../reference.md)

---

## Attr: ExportSpec.caption

### Description
Optional caption rendered above the sheet's header row. The export may append further caption lines of its own, such as the "Filtered by:" statement.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: ExportSpec.fields

### Description
The sheet's columns, in order: objects with `name` (the property read from each row or fetched record), `title` (the rendered column header), and optional `type` and `format` hints the export engine uses to pick cell formats.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: ExportSpec.fetch

### Description
The sheet's data **by reference**: a fetch the server executes — `dataSource`, `criteria`, `operationId`, `sortBy`, `groupBy` / `summaryFunctions`. Mutually exclusive with [ExportSpec.rows](#attr-exportspecrows).

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: ExportSpec.dsName

### Description
ID of the DataSource the sheet's data comes from.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: ExportSpec.rows

### Description
The sheet's data **by value**: the records themselves, computed on the client. Mutually exclusive with [ExportSpec.fetch](#attr-exportspecfetch).

### Groups

- descendantDataExport

**Flags**: IR

---
