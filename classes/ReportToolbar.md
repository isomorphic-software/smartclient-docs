# ReportToolbar Documentation

[← Back to API Index](../reference.md)

---

## Class: ReportToolbar

### Description
The report-level consumer toolbar for a deployed [DataReport](DataReport.md#class-datareport): whole-report actions a viewer invokes (Export, Restore Hidden, and a "data as of" freshness label). It is an autoChild of [ReportScreen](ReportScreen.md#class-reportscreen) and drives that screen's DataReport. The runtime analog of ReportBuilder's authoring toolbar; per-action visibility is controlled by flags ([ReportToolbar.showExport](#attr-reporttoolbarshowexport) etc.). Export is built as a menu button from the start so added capture formats (PDF / image) are additive, not a relayout.

---
## Attr: ReportToolbar.showRestoreHidden

### Description
Whether the dynamic "Show Hidden" control is available. When true (the default) it appears automatically whenever the deployed report has components the viewer has hidden, listing them for re-show; set false to suppress it entirely.

**Flags**: IR

---
## Attr: ReportToolbar.untitledComponentTitle

### Description
Menu label for a hidden component that has no title of its own.

**Flags**: IR

---
## Attr: ReportToolbar.showAllTitle

### Description
Menu entry (below the individual components) that re-shows every hidden component at once.

**Flags**: IR

---
## Attr: ReportToolbar.editModeActionDisabledPrompt

### Description
Hover hint shown on each report-toolbar action button while the report is open in an editor. The actions are a disabled preview there -- they run against the deployed report, not the editor -- so each button is individually disabled and carries this prompt (rather than disabling the whole toolbar with a single cluster-level hint).

**Flags**: IR

---
## Attr: ReportToolbar.restoreHiddenTitle

### Description
Base title of the dynamic control that re-shows viewer-hidden components; the current hidden count is appended, e.g. "Show Hidden (2)".

**Flags**: IR

---
## Attr: ReportToolbar.titleEditPrompt

### Description
Hover hint shown on the report title while editing, cueing that a double-click renames it inline. Blank to suppress the hint.

**Flags**: IR

---
## Method: ReportToolbar.exportReport

### Description
Export the whole report (xlsx today).

---
## Method: ReportToolbar.restoreAll

### Description
Re-show all viewer-hidden components.

---
## Method: ReportToolbar.restoreHidden

### Description
Synonym for [ReportToolbar.restoreAll](#method-reporttoolbarrestoreall).

---
## Method: ReportToolbar.restore

### Description
Re-show one viewer-hidden component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the hidden component to re-show |

---
