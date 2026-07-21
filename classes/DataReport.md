# DataReport Documentation

[← Back to API Index](../reference.md)

---

## Class: DataReport

### Description
A runtime report document: a [PortalLayout](PortalLayout.md#class-portallayout) whose portlets are the report's data components (grids, charts, KPIs, pivots, detail views). DataReport owns the data-facing behavior a report needs whether or not an editor is present -- most importantly gathering the report's data and exporting the whole report to Excel.

[ReportBuilder](ReportBuilder.md#class-reportbuilder) is the _editor_ for a DataReport: it hosts one as the root of its edit canvas and delegates export to it, so a report exports identically whether driven from the builder or deployed standalone.

---
## Method: DataReport.getComponents

### Description
The report's components, one descriptor per portlet, in portlet (visual) order. Each descriptor is shaped like a Reify edit node (`{ type, liveObject, title, exportInclude, defaults:{title, exportInclude} }`) so the export pipeline reads one shape whether enumeration comes from a live PortalLayout (deployed) or, in the editor, from [ReportBuilder](ReportBuilder.md#class-reportbuilder) delegating here. Filtered to the classified component types; a portlet with no recognized inner component is skipped.

### Returns

`[Array](#type-array)` — component descriptors, in report order

---
## Method: DataReport.exportReportToExcel

### Description
Export the whole report to a single multi-sheet Excel workbook -- one sheet per included data component -- and download it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | true | — | fired once the download request has been submitted |

---
## Method: DataReport.restore

### Description
Re-show a single component the viewer has hidden (see [DataReport.willClosePortlet](#method-datareportwillcloseportlet)), returning it to the layout position implied by where its recorded neighbor now sits.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | a portlet currently in [DataReport.getHiddenPortlets](#method-datareportgethiddenportlets) |

---
## Method: DataReport.getHiddenPortlets

### Description
The portlets currently hidden by the viewer, in the order they were hidden.

### Returns

`[Array of Portlet](#type-array-of-portlet)` — hidden portlets (empty if none)

---
## Method: DataReport.restoreAll

### Description
Re-show every component the viewer has hidden, reconstructing the original layout.

---
## Method: DataReport.restoreHidden

### Description
Re-show every viewer-hidden component. Synonym for [DataReport.restoreAll](#method-datareportrestoreall).

---
## Method: DataReport.setReportTitle

### Description
Sets the report's display [DataReport.reportTitle](#datareportreporttitle): the header title (shown by the enclosing ReportScreen's toolbar) and the export base name. In an editor this writes THROUGH the edit node, so the new title serializes into the saved / published report and reaches the deployed header; the toolbar then refreshes to show it. This is the report's DISPLAY title, distinct from the saved-report NAME the ReportBuilder Save dialog manages -- two reports may share a title but have different names.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [String](#type-string) | false | — | new display title, or null to fall back to the untitled default |

---
