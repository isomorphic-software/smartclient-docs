# Descendant Data Export

[← Back to API Index](../reference.md)

---

## KB Topic: Descendant Data Export

### Description
Any [Canvas](../classes/Canvas_1.md#class-canvas) can export the data of the [DataBoundComponent](../reference.md#interface-databoundcomponent)s beneath it as one multi-sheet Excel workbook via [Canvas.exportDescendantData](../classes/Canvas_1.md#method-canvasexportdescendantdata) — the main reference for this feature. Each component's sheet is produced by running that component's own effective fetch against its DataSource, so the workbook reflects stored data, and a cover sheet states every filter that narrows the result.

Per-component control is declarative: [shouldExport](../classes/DataBoundComponent.md#attr-databoundcomponentshouldexport) governs participation, [exportTitle](../classes/DataBoundComponent.md#attr-databoundcomponentexporttitle) names the sheet, and [exportAsDisplayed](../classes/DataBoundComponent.md#attr-databoundcomponentexportasdisplayed) switches a component to exporting its displayed values instead. Per-call configuration is passed as [MultiSheetExportSettings](../reference_2.md#object-multisheetexportsettings).

### Related

- [Canvas.exportDescendantData](../classes/Canvas_1.md#method-canvasexportdescendantdata)
- [DataBoundComponent.getExportSpec](../classes/DataBoundComponent.md#method-databoundcomponentgetexportspec)
- [MultiSheetExportSettings](../reference_2.md#object-multisheetexportsettings)
- [ExportSpec](../reference_2.md#object-exportspec)
- [MultiSheetExportSettings.title](../classes/MultiSheetExportSettings.md#attr-multisheetexportsettingstitle)
- [MultiSheetExportSettings.exportFilename](../classes/MultiSheetExportSettings.md#attr-multisheetexportsettingsexportfilename)
- [MultiSheetExportSettings.includeHidden](../classes/MultiSheetExportSettings.md#attr-multisheetexportsettingsincludehidden)
- [MultiSheetExportSettings.maxExportRows](../classes/MultiSheetExportSettings.md#attr-multisheetexportsettingsmaxexportrows)
- [MultiSheetExportSettings.labels](../classes/MultiSheetExportSettings.md#attr-multisheetexportsettingslabels)
- [MultiSheetExportSettings.callback](../classes/MultiSheetExportSettings.md#attr-multisheetexportsettingscallback)
- [DataBoundComponent.shouldExport](../classes/DataBoundComponent.md#attr-databoundcomponentshouldexport)
- [DataBoundComponent.exportTitle](../classes/DataBoundComponent.md#attr-databoundcomponentexporttitle)
- [DataBoundComponent.exportAsDisplayed](../classes/DataBoundComponent.md#attr-databoundcomponentexportasdisplayed)
- [ExportSpec.fields](../classes/ExportSpec.md#attr-exportspecfields)
- [ExportSpec.caption](../classes/ExportSpec.md#attr-exportspeccaption)
- [ExportSpec.fetch](../classes/ExportSpec.md#attr-exportspecfetch)
- [ExportSpec.rows](../classes/ExportSpec.md#attr-exportspecrows)
- [ExportSpec.dsName](../classes/ExportSpec.md#attr-exportspecdsname)

### See Also

- [exporting](exporting.md#kb-topic-exporting)
- [chartExport](chartExport.md#kb-topic-chart-data-export)
- [exportFormatting](exportFormatting.md#kb-topic-export-value-formatting)

---
