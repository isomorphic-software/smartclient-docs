# MultiSheetExportSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: MultiSheetExportSettings.includeHidden

### Description
By default only visible components are exported — the export captures the view the user is looking at. Set this to export hidden eligible components as well.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: MultiSheetExportSettings.maxExportRows

### Description
Maximum rows a client-executed fetch may export. When a component's fetch would exceed it, the export is refused with [Canvas.exportRowLimitMessage](Canvas_1.md#attr-canvasexportrowlimitmessage) before any download begins. Fetches executed by the SmartClient Server are bounded by the server's own configured limit instead.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: MultiSheetExportSettings.title

### Description
Title shown on the workbook's cover sheet. When unset, falls back to [Canvas.exportDefaultTitle](Canvas_1.md#attr-canvasexportdefaulttitle).

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: MultiSheetExportSettings.callback

### Description
Fired once the export request has been submitted. The workbook downloads through the browser's file transport, which reports nothing back to the page, so this callback does not indicate the download has completed — only that it was initiated.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: MultiSheetExportSettings.labels

### Description
Per-call overrides for the cover and caption label strings. Property names and defaults come from the corresponding canvas attributes — [Canvas.filtersAppliedTitle](Canvas_1.md#attr-canvasfiltersappliedtitle), [Canvas.filterConditionTitle](Canvas_1.md#attr-canvasfilterconditiontitle), [Canvas.filterAppliesToTitle](Canvas_1.md#attr-canvasfilterappliestotitle), [Canvas.allSheetsMessage](Canvas_1.md#attr-canvasallsheetsmessage), [Canvas.noFiltersAppliedMessage](Canvas_1.md#attr-canvasnofiltersappliedmessage), [Canvas.asDisplayedMessage](Canvas_1.md#attr-canvasasdisplayedmessage) and [Canvas.asDisplayedPartialMessage](Canvas_1.md#attr-canvasasdisplayedpartialmessage); set those attributes instead to change the wording for every export.

### Groups

- descendantDataExport

**Flags**: IR

---
## Attr: MultiSheetExportSettings.exportFilename

### Description
Base name for the downloaded file (the `.xlsx` extension is appended). When unset, a filesystem-safe name is derived from [MultiSheetExportSettings.title](#attr-multisheetexportsettingstitle).

### Groups

- descendantDataExport

**Flags**: IR

---
