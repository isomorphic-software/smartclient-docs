# Exporting

[← Back to API Index](../reference.md)

---

## KB Topic: Exporting

### Description
SmartClient can export both the **data** behind components and the **visual appearance** of components, through a family of APIs that share formatting rules and delivery mechanics. This topic maps the family; each linked API documents its own details.
#### Data vs. visuals
Exporting _data_ produces spreadsheet / CSV / JSON / XML output built from records — the subject of the rest of this topic. Exporting _visuals_ produces a PDF or image of components as rendered: see [RPCManager.exportContent](../classes/RPCManager.md#classmethod-rpcmanagerexportcontent) for print-quality PDF of any component tree, [RPCManager.exportImage](../classes/RPCManager.md#classmethod-rpcmanagerexportimage) for images of drawn content, and the [Printing](printing.md#kb-topic-printing) overview for the underlying system.
#### Exporting one component's data
The central choice is **whose values the file holds**:

*   [exportData()](../classes/DataBoundComponent.md#method-databoundcomponentexportdata) is **server-driven**: the server re-runs the component's fetch and builds the file from _stored_ values — the full filtered dataset, not just the rows loaded on the client. Configure it through [DSRequest export properties](../classes/DSRequest.md#attr-dsrequestexportas) and field-level export attributes.
*   [exportClientData()](../classes/ListGrid_2.md#method-listgridexportclientdata) is **client-driven**: the data is gathered exactly _as displayed_ — formatters, formula and summary fields, hilites — and the server only converts it to the requested file format.

The rules for when declared formats apply during each kind of export, and how to override them, are the subject of [Export Value\\n Formatting](exportFormatting.md#kb-topic-export-value-formatting). A DataSource can also export with no component involved, via [DataSource.exportData](../classes/DataSource_1.md#method-datasourceexportdata).
#### Exporting many components — one workbook
[Canvas.exportDescendantData](../classes/Canvas_1.md#method-canvasexportdescendantdata) exports every eligible [DataBoundComponent](../reference.md#interface-databoundcomponent) beneath a container as one multi-sheet Excel workbook, led by a cover sheet stating the filters that narrow each sheet. Components control their participation and naming declaratively ([shouldExport](../classes/DataBoundComponent.md#attr-databoundcomponentshouldexport), [exportTitle](../classes/DataBoundComponent.md#attr-databoundcomponentexporttitle)), and [exportAsDisplayed](../classes/DataBoundComponent.md#attr-databoundcomponentexportasdisplayed) switches a component's sheet to the same as-displayed gathering `exportClientData()` uses. See [Descendant Data Export](descendantDataExport.md#kb-topic-descendant-data-export) for the full treatment.
#### Components that reshape their export
A component's faithful export is not always its raw fetched records. Each component contributes its sheet through [getExportSpec()](../classes/DataBoundComponent.md#method-databoundcomponentgetexportspec), returning an [ExportSpec](../reference_2.md#object-exportspec): the sheet's columns and caption, plus its data either **by reference** (a fetch the server executes) or **by value** (rows computed on the client). Override it to substitute a semantically richer table — the shipped example is [FacetChart](../classes/FacetChart.md#class-facetchart), which exports the table its chart conveys rather than its raw fetch: see [Chart Data Export](chartExport.md#kb-topic-chart-data-export).
#### Formats and delivery
[ExportFormat](../reference_2.md#type-exportformat) lists the file formats and [ExportDisplay](../reference_2.md#type-exportdisplay) chooses download versus inline display. [DataSource.exportMultiSheetData](../classes/DataSource.md#classmethod-datasourceexportmultisheetdata) is the multi-sheet engine's entry point for assembling a workbook programmatically.

### See Also

- [exportFormatting](exportFormatting.md#kb-topic-export-value-formatting)
- [descendantDataExport](descendantDataExport.md#kb-topic-descendant-data-export)
- [chartExport](chartExport.md#kb-topic-chart-data-export)
- [printing](printing.md#kb-topic-printing)
- [excelPasting](excelPasting.md#kb-topic-copy-and-paste-with-excel)
- [exportBGColor](exportBGColor.md#kb-topic-exports--cell-background-color)
- [backgroundDownload](backgroundDownload.md#kb-topic-background-download)

---
