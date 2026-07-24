# ReportBuilder Documentation

[← Back to API Index](../reference.md)

---

## Class: ReportBuilder

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A component for building data-driven reports using drag-and-drop composition and AI assistance. ReportBuilder provides a visual interface for creating reports from available DataSources, with support for AI-powered component generation via natural language prompts.

The component includes:

*   A toolbar with Save, Load, Export, and New Report actions
*   A DataSource picker to select which DataSources are available for reporting
*   An AI prompt area for natural language report creation
*   A component palette for drag-and-drop report composition
*   An EditPane with PortalLayout for visual arrangement of report components

---
## Attr: ReportBuilder.paletteWidth

### Description
Width of the left palette panel containing the DataSource picker, AI prompt, and component palette.

**Flags**: IRW

---
## Attr: ReportBuilder.reportLoaded

### Description
Notification fired after a report is successfully loaded.

Signature: `reportLoaded(report)` where `report` is the loaded report record (`Object`).

**Flags**: IRW

---
## Attr: ReportBuilder.showTheme

### Description
Whether the "Theme" toolbar menu button is shown.

**Flags**: IR

---
## Attr: ReportBuilder.editArea

### Description
Right panel containing the EditPane and optional PropertySheet.

**Flags**: R

---
## Attr: ReportBuilder.showExportToExcel

### Description
Whether the "Export to Excel" button is shown on the ReportBuilder's own header. This is an authoring convenience: the report's ReportToolbar Export is a disabled preview while editing (it runs against the deployed report), so this button lets an author export the whole report to a multi-sheet workbook without publishing first.

**Flags**: IR

---
## Attr: ReportBuilder.palettePanel

### Description
Left panel containing the AI prompt form and the Components group (DataSource picker + component palette).

**Flags**: R

---
## Attr: ReportBuilder.reportLoadDialog

### Description
Dialog for browsing and loading saved reports.

**Flags**: R

---
## Attr: ReportBuilder.aiEnabled

### Description
Whether AI-powered report creation is enabled. When true, the AI prompt form is shown and users can create reports via natural language requests.

**Flags**: IRW

---
## Attr: ReportBuilder.aiIncompleteReasonLabel

### Description
Label above the bulleted reason list in the incomplete dialog.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.slicerFieldForm

### Description
Form within [ReportBuilder.slicerFieldDialog](#attr-reportbuilderslicerfielddialog) holding the field- selection SelectItem. Its valueMap is populated per drop with the sliceable fields of the selected DataSource.

**Flags**: R

---
## Attr: ReportBuilder.aiProcessLogAutoHideDelay

### Description
Milliseconds to wait after the AI process completes before hiding the [AI process log](#attr-reportbuilderaiprocesslog) overlay automatically. The delay gives the user time to see the final "Done." (or failure) row before the window disappears; set to 0 to leave the log open until dismissed manually.

**Flags**: IRW

---
## Attr: ReportBuilder.suggestedPrompts

### Description
Optional list of natural-language prompt strings deployments want authors to discover. Surfaced in the AI prompt input's history grid as "suggested" rows alongside actual prompt history. Suggestions are not per-DataSource — the AI sees every available DataSource regardless of the picker selection, so suggested prompts are equally relevant across the catalog.

**Flags**: IRW

---
## Attr: ReportBuilder.globalFilterDateField

### Description
Name of the date/datetime field driven by the report-level date-range filter in the global filter bar. The selected range is published to the report [dataContext](Canvas.md#attr-canvasdatacontext) for every available DataSource that has a field of this name, so a single date range narrows all data views at once. Defaults to `"created"` -- the row audit timestamp present on the demo's DataSources. A DataSource without this field is simply left unfiltered by the date range.

**Flags**: IRW

---
## Attr: ReportBuilder.reportSaveForm

### Description
Form within the save dialog for entering report metadata.

**Flags**: R

---
## Attr: ReportBuilder.dataSourcePickerForm

### Description
Form containing the DataSource picker. Scoped to manual palette-based component creation only (sets the default DataSource for newly-dropped grids and charts); the AI flow ignores this selection and is given every available DataSource so it can pick the most appropriate one for the user's prompt.

**Flags**: R

---
## Attr: ReportBuilder.autoLinkComponents

### Description
When true, dropping two foreign-key-related data views (e.g. an Orders grid and an Order Items grid) automatically creates a master-detail link: selecting a row in the master (the FK parent) re-fetches the detail (the FK child) to that record's children via [DataBoundComponent.fetchRelatedData](#method-databoundcomponentfetchrelateddata). Auto-links surface an auto-dismissing notification and a "Driven by" affordance, and can be changed or removed by the user (which marks the link explicit, so a later auto-link pass leaves it alone). Turn this off for fully manual linking.

**Flags**: IRW

---
## Attr: ReportBuilder.showUndo

### Description
Whether the "Undo" toolbar button is shown.

**Flags**: IR

---
## Attr: ReportBuilder.allowedComponentTypes

### Description
Component types available in the palette for report building. These are organized into categories: Data Views (standalone, use DS picker), Detail Views (linked to a parent component), and Layout (non-data-bound).

**Flags**: IRW

---
## Attr: ReportBuilder.editPane

### Description
Visual composition surface for report components.

**Flags**: R

---
## Attr: ReportBuilder.chartConfigDialog

### Description
Dialog for configuring chart facets, measures, and aggregation. Created as a top-level modal window that auto-centers on screen.

**Flags**: R

---
## Attr: ReportBuilder.aiPromptLayout

### Description
Layout hosting the compact AI prompt input. Collapsed by default it shows a one-line TextArea + Submit + expand chevron in roughly 50px; expanded it grows the TextArea to several rows and reveals a history grid populated from [ReportBuilder.historyDataSource](#attr-reportbuilderhistorydatasource) merged with [ReportBuilder.suggestedPrompts](#attr-reportbuildersuggestedprompts).

**Flags**: R

---
## Attr: ReportBuilder.showEditInReify

### Description
Whether the "Edit in Reify" toolbar button is shown. Defaults to the value of [ReportBuilder.reifyIntegration](#attr-reportbuilderreifyintegration).

**Flags**: IR

---
## Attr: ReportBuilder.historyKey

### Description
Override the auto-generated localStorage scope key. Defaults to `"reportBuilder.aiPromptHistory.`<reifyProjectName or 'default'>`"`. Has no effect when [ReportBuilder.historyDataSource](#attr-reportbuilderhistorydatasource) is configured to a real server-backed DataSource.

**Flags**: IRW

---
## Attr: ReportBuilder.aiIncompleteSummaryLabel

### Description
Label above [output.summary](#outputsummary) in the incomplete dialog. Only rendered when the CoT supplied a summary.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.historyMax

### Description
Cap on persisted AI prompt history records. Older records are trimmed in FIFO order once the cap is reached.

**Flags**: IRW

---
## Attr: ReportBuilder.aiIncompleteSubtitle

### Description
Subtitle text in the incomplete dialog.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.aiIncompletePromptLabel

### Description
Label above the original prompt in the incomplete dialog.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.reportSaved

### Description
Notification fired after a report is successfully saved.

Signature: `reportSaved(report)` where `report` is the saved report record (`Object`).

**Flags**: IRW

---
## Attr: ReportBuilder.scheduleRecipientOptions

### Description
Suggested recipient email addresses offered in the Schedule dialog's recipients picker. Empty by default; a deployment supplies its own distribution lists / known addresses. Users may still type any valid email (validated on entry).

**Flags**: IRW

---
## Attr: ReportBuilder.defaultExportFormat

### Description
Default format for report export.

**Flags**: IRW

---
## Attr: ReportBuilder.aiTimeoutMessage

### Description
Synthesized error message used when the watchdog timer fires.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.componentLinks

### Description
Tracks links between components. Each link has sourceComponentId, targetComponentId, linkType (selection|foreignKey|drillDown), and field mappings.

**Flags**: IRW

---
## Attr: ReportBuilder.componentsGroup

### Description
Group wrapping the DataSource picker and the component palette. Both belong to the manual palette-based component-creation workflow, so they are grouped together visually and scoped consistently below the separate AI section.

**Flags**: R

---
## Attr: ReportBuilder.portalLayout

### Description
Default paletteNode for the PortalLayout used within the EditPane.

**Flags**: R

---
## Attr: ReportBuilder.dsDataSource

### Description
DataSource used for DataSource definition storage. Defaults to `vbDataSources` (Reify's on-prem ProjectFile fileSource). Hosted environments can point at `isc_hostedDataSources`. ReportBuilder and Reify share this storage so that Edit-in-Reify and Publish flows find the DataSources automatically.

**Flags**: IR

---
## Attr: ReportBuilder.reifyProjectName

### Description
Name of the Reify project into which reports are written by [ReportBuilder.editInReify](#method-reportbuildereditinreify). If the project does not exist in Reify storage (`vbProjects`) it is created on the first save; on subsequent saves the new screen is appended to the existing project's screen list.

**Flags**: IRW

---
## Attr: ReportBuilder.aiEngineId

### Description
AI engine ID to use for AI-powered component generation. If not specified, inherits from [AI.defaultEngineId](AI.md#classattr-aidefaultengineid).

**Flags**: IRW

---
## Attr: ReportBuilder.availableDataSources

### Description
DataSource IDs available for report building. These DataSources appear in the DS picker dropdown and are included in published and Edit-in-Reify screens so that indirectly referenced DataSources (via `includeFrom`, `foreignKey`, etc.) are available at runtime.

The DataSource definitions must exist in [ReportBuilder.dsDataSource](#attr-reportbuilderdsdatasource) storage (typically `vbDataSources`). They are loaded on demand via `DataSourceLoader` when the picker initializes.

This property is effectively required — without it ReportBuilder has no DataSources for its reports.

**Flags**: IRW

---
## Attr: ReportBuilder.aiNoOutputMessage

### Description
Notify text shown when the CoT calls [finished](#finished) with no output object.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.aiIncompleteKeepButtonTitle

### Description
"Keep Anyway" button title - accepts the partial result and raises the persistent incomplete badge on the AI prompt header.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.aiTimeoutMillis

### Description
Watchdog timeout for the [ReportBuilderProcess](#class-reportbuilderprocess) CoT. If the process doesn't call [finished](#finished) within this many milliseconds, ReportBuilder synthesizes an [ReportBuilder.aiTimeoutMessage](#attr-reportbuilderaitimeoutmessage) error and routes it through the standard failure handler so the loading indicator clears and the user gets a Retry affordance. Set to 0 or a negative value to disable the watchdog.

**Flags**: IRW

---
## Attr: ReportBuilder.exportFormats

### Description
Available export formats for reports.

**Flags**: IRW

---
## Attr: ReportBuilder.aiPromptForm

### Description
Form for entering AI prompts to generate report components. Holds the prompt TextArea, Submit button, and expand chevron in a single row.

**Flags**: R

---
## Attr: ReportBuilder.defaultPortalColumns

### Description
Initial number of columns in the PortalLayout. Additional columns are created automatically when dragging components to the right edge, and empty columns are removed automatically.

**Flags**: IRW

---
## Attr: ReportBuilder.supportingDataSources

### Description
Additional DataSource IDs to load for every report screen that should **not** appear in the DataSource picker. Unlike [ReportBuilder.availableDataSources](#attr-reportbuilderavailabledatasources) — the DataSources an author actually builds report components on — supporting DataSources exist only to make the available ones work correctly at runtime: they supply the related DataSources that [DataSourceField.includeFrom](DataSourceField.md#attr-datasourcefieldincludefrom) fields, [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) links, and cross-DataSource [Slicer](Slicer.md#class-slicer) criteria resolve against. Without them, includeFrom fields log "related DataSource does not exist" / "cannot be resolved" warnings and cross-DataSource filters silently match no records.

Supporting DataSources are loaded (via `isc.DataSource.load()`) alongside `availableDataSources`, and are included in the `loadID` declarations of published and Edit-in-Reify screens so they are present at runtime in those views. When a report is opened in Reify, supporting DataSources are treated no differently from available ones — a developer editing the screen there can bind new components to them. The distinction exists only within ReportBuilder itself, which hides them from the author's DataSource picker to keep the build list focused.

Like `availableDataSources`, these definitions must exist in [ReportBuilder.dsDataSource](#attr-reportbuilderdsdatasource) storage.

**Flags**: IRW

---
## Attr: ReportBuilder.parameterFields

### Description
Field definitions for report-level parameters. These appear in a parameter form above the report and filter all data-bound components.

**Flags**: IRW

---
## Attr: ReportBuilder.showPublish

### Description
Whether the "Publish" toolbar button is shown. When `true` and [ReportBuilder.reifyIntegration](#attr-reportbuilderreifyintegration) is `false`, a [ReportBuilder.publishHandler](#attr-reportbuilderpublishhandler) must be provided (otherwise the button has no target).

**Flags**: IR

---
## Attr: ReportBuilder.componentCreated

### Description
Notification fired after a component is added to the report.

Signature: `componentCreated(editNode, paletteNode)` where:

*   `editNode` - the created [EditNode](../reference.md#object-editnode)
*   `paletteNode` - the source [PaletteNode](../reference.md#object-palettenode)

**Flags**: IRW

---
## Attr: ReportBuilder.publishHandler

### Description
Custom handler invoked by [ReportBuilder.publishReport](#method-reportbuilderpublishreport) instead of the default `isc.Reify.publishScreen()` flow. Receives two arguments:

*   `reportSource` — the serialized report XML from [ReportBuilder.getReportDefinition](#method-reportbuildergetreportdefinition)
*   `reportName` — the current report title (may be `null` for an unsaved report)

Use this to implement a non-Reify publish action such as showing the live report and its source in a popup window.

**Flags**: IR

---
## Attr: ReportBuilder.aiProcessLog

### Description
Non-blocking overlay window that surfaces the running [ReportBuilderProcess](#class-reportbuilderprocess) as a per-task progress log. Created lazily on the first AI submission and re-attached (via [CoTProcessLog.setProcess](CoTProcessLog.md#method-cotprocesslogsetprocess)) on every subsequent run. The "AI is working…" inline label remains as the always-on, low-attention indicator; this widget is opt-in detail for users who want to see what the AI is doing step-by-step.

The log auto-hides shortly after the process completes (success or failure) so the canvas isn't permanently obstructed; the user can also close or minimize it at any time without affecting the AI run.

**Flags**: R

---
## Attr: ReportBuilder.reifyIntegration

### Description
Master switch for Reify integration. When `false`, no `isc.Reify.*` call is reachable and the Reify module is never lazy-loaded. Sets the defaults for [ReportBuilder.showEditInReify](#attr-reportbuildershoweditinreify) and [ReportBuilder.showPublish](#attr-reportbuildershowpublish).

Set this to `false` for standalone use under an Enterprise (Portals & Tools) license with no Reify dependency.

**Flags**: IR

---
## Attr: ReportBuilder.aiErrorTitle

### Description
Title for the dialog shown on hard AI failure (error output, empty output, watchdog timeout, synchronous throw).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.componentPalette

### Description
Palette containing available component types. Data Views are standalone components that use the DataSource picker. Uses ListPalette so that setDefaultPalette works correctly and the framework handles drop positioning automatically.

**Flags**: R

---
## Attr: ReportBuilder.gridAdvancedFilter

### Description
Whether ListGrid components dropped into a report are configured with the advanced [FilterBuilder](FilterBuilder.md#class-filterbuilder) window enabled -- accessed from a grid header's "Filter using" -> "Advanced Filtering" menu -- including **aggregate** (summary sub-query) criteria ([Criterion.fieldQuery](Criterion.md#attr-criterionfieldquery) / [Criterion.valueQuery](Criterion.md#attr-criterionvaluequery)). This lets a report author build nested and aggregate filters such as "partners whose total order value > 100k" directly on a grid.

Aggregate criteria resolve client-side against cached data, so this works on the demo's `clientOnly` DataSources without a server. Defaults to `true`; set `false` to keep dropped grids on the plain filter editor only.

**Flags**: IRW

---
## Attr: ReportBuilder.toolbar

### Description
ToolStrip providing report-level actions: Save, Load, Export, New, etc.

**Flags**: R

---
## Attr: ReportBuilder.historyDataSource

### Description
DataSource ID (or DataSource instance) to persist AI prompt history into. If unset, ReportBuilder auto-creates a [LocalDataSource](#class-localdatasource) keyed by [ReportBuilder.historyKey](#attr-reportbuilderhistorykey) so prompt history survives page reloads on the local browser. Setting this to a server-backed DataSource ID swaps in cross-device persistence with no other code changes.

**Flags**: IRW

---
## Attr: ReportBuilder.aiErrorRetryButtonTitle

### Description
"Retry" button title in the error dialog. Re-submits the original prompt verbatim.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.scheduleTimeZones

### Description
Optional override for the Schedule dialog's time-zone list: a valueMap of IANA zone id to friendly "Location (Zone Name)" display. When null, [SchedulerItem](#class-scheduleritem)'s curated default (major world zones) is used; set this to offer a smaller / custom set.

**Flags**: IRW

---
## Attr: ReportBuilder.mainLayout

### Description
Main horizontal layout containing the palette panel and edit area.

**Flags**: R

---
## Attr: ReportBuilder.aiIncompleteEditButtonTitle

### Description
"Edit & Retry" button title - re-populates the prompt for editing.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.reportSaveDialog

### Description
Dialog for saving reports with title and description.

**Flags**: R

---
## Attr: ReportBuilder.aiIncompleteTitle

### Description
Title for the dialog shown when the AI flow finishes with [output.incomplete](#outputincomplete)=true.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ReportBuilder.componentDefaults

### Description
A map of component class name to a block of default properties applied to every component of that class created in this ReportBuilder -- whether added by the user (palette drag or double-click) or by the AI. The keys are SmartClient class names, matching the component types the palette offers (see [ReportBuilder](#class-reportbuilder) data / detail / layout view types).

ReportBuilder ships built-in per-class defaults (for example a Grid's `showFilterEditor`, or a TileGrid's tile sizing). Values you provide here are merged OVER those built-ins, so you can either add new class-wide defaults or override the built-in ones. The resulting block is then applied as the **base** for each new component -- merged UNDER the dynamically-calculated structural defaults (`dataSource`, computed facets / fields) and the user's or AI's own picks, so those always win and are never clobbered. Effectively:

```
   isc.addProperties({}, builtin[type], componentDefaults[type], structuralConfig)
 
```
Example -- roomier pivot headers, and no filter editor on grids:
```
   componentDefaults: {
       CubeGrid: { defaultRowFacetWidth: 160, facetHeight: 28 },
       ListGrid: { showFilterEditor: false }
   }
 
```
Restored (saved) reports are not re-defaulted -- these apply only to newly created components.

**Flags**: IRW

---
## Attr: ReportBuilder.reportDataSource

### Description
DataSource for persisting saved reports. If not specified, reports can only be saved to local storage or exported.

**Flags**: IRW

---
## Attr: ReportBuilder.showRedo

### Description
Whether the "Redo" toolbar button is shown.

**Flags**: IR

---
## Attr: ReportBuilder.slicerFieldDialog

### Description
Modal dialog shown when a Slicer palette node is dropped, prompting the author to choose which DataSource field the slicer targets. Created lazily on the first Slicer drop and reused; its field picker and the per-drop context are refreshed for each drop before the dialog is shown.

**Flags**: R

---
## Attr: ReportBuilder.aiPromptTextBoxStyle

### Description
Optional override for the [TextAreaItem.textBoxStyle](TextAreaItem.md#attr-textareaitemtextboxstyle) of the "Ask AI..." prompt input, so embedders can theme it without touching the rest of the framework's textArea styles. Picks up the standard SmartClient state suffixes (_Focused_, _Disabled_, _Error_, _Hint_) - define those alongside the base class. When unset, the prompt uses the framework's default `textAreaItem` style.

**Flags**: IRW

---
## Attr: ReportBuilder.showPlaceholderNodes

### Description
Whether work-in-progress "placeholder" palette nodes -- nodes that drop an inert labelled box rather than a working component -- are shown in the component palette. Defaults to `false` so the palette contains only nodes that produce a real, data-bound component. Set `true` during development to surface placeholder nodes for later-phase components.

**Flags**: IRW

---
## Attr: ReportBuilder.reportLoadGrid

### Description
Grid showing available reports in the load dialog.

**Flags**: R

---
## Method: ReportBuilder.newReport

### Description
Clears the current report and creates a new blank report.

---
## Method: ReportBuilder.saveReportAs

### Description
Saves the current report as a NEW report (or template), leaving any previously-saved report untouched. Use this to derive a separate template from a report (or vice versa) instead of overwriting it in place, which is what plain [ReportBuilder.saveReport](#method-reportbuildersavereport) does for an existing report.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired after the save |

---
## Method: ReportBuilder.exportReportToExcel

### Description
Exports the whole report as a multi-sheet .xlsx workbook -- the "data behind the report". Gathers a self-contained export model from the live report components (a working-model workbook), hands it to the static [DataSource.exportMultiSheetData](DataSource.md#classmethod-datasourceexportmultisheetdata), whose built-in server method builds the workbook with Apache POI and streams the result back so the browser downloads it. Slicer semantics: the live components already reflect any slicer filters applied in the report, so the rows we gather are the pre-filtered ("baked") data -- the author-fixed-filter model.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | true | — | fired after the export request completes |

---
## Method: ReportBuilder.setReportDefinition

### Description
Loads a serialized report definition.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| definition | [String](#type-string) | false | — | serialized report XML |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired after load completes |

---
## Method: ReportBuilder.isReportDirty

### Description
Returns whether the report has unsaved changes since it was last created, loaded, or saved.

### Returns

`[boolean](../reference.md#type-boolean)` — true if there are unsaved changes

---
## Method: ReportBuilder.loadReport

### Description
Opens a dialog to load a previously saved report.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired after load completes |

---
## Method: ReportBuilder.addComponent

### Description
Adds a component to the report from a paletteNode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNode | [PaletteNode](#type-palettenode) | false | — | the palette node to add |

### Returns

`[EditNode](#type-editnode)` — the created EditNode

---
## Method: ReportBuilder.getReportQuery

### Description
Returns the current report-level query configuration.

### Returns

`[DSRequest Properties](#type-dsrequest-properties)` — current query configuration

---
## Method: ReportBuilder.exportReport

### Description
Exports the current report to a file.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [String](#type-string) | true | — | export format (pdf, xlsx, csv, png). Defaults to defaultExportFormat. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired after export completes |

---
## Method: ReportBuilder.getComponentDefaults

### Description
Returns the effective componentDefaults block for a component class: the framework built-in defaults for that class with any [ReportBuilder.componentDefaults](#attr-reportbuildercomponentdefaults) overrides merged over them. Never returns null, so callers can merge the result unconditionally.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | SmartClient class name, e.g. `"CubeGrid"` |

### Returns

`[Object](../reference.md#type-object)` — a copy of the effective defaults block (never null)

---
## Method: ReportBuilder.saveReport

### Description
Saves the current report. If a reportDataSource is configured, opens the save dialog. Otherwise, prompts the user to export the report.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired after save completes |

---
## Method: ReportBuilder.removeComponent

### Description
Removes a component from the report.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editNode | [EditNode](#type-editnode) | false | — | the EditNode to remove |

---
## Method: ReportBuilder.getComponents

### Description
Returns the report's components as edit-node-shaped descriptors, one per portlet, in report order. Delegates to the [DataReport](DataReport.md#class-datareport) root, which enumerates its live portlets -- so the same list is produced whether the report is edited here or deployed standalone. See [DataReport.getComponents](DataReport.md#method-datareportgetcomponents).

### Returns

`[Array](#type-array)` — component descriptors

---
## Method: ReportBuilder.getReportDefinition

### Description
Returns the serialized report definition.

### Returns

`[String](#type-string)` — serialized report XML

---
## Method: ReportBuilder.editInReify

### Description
Opens the current report in Reify for advanced editing. The current report's [EditContext](EditContext.md#class-editcontext) is serialized and saved to Reify's screen storage (`vbScreens`) under a timestamp-suffixed screen name, the screen is added to the [ReportBuilder.reifyProjectName](#attr-reportbuilderreifyprojectname) project (creating it if necessary), then Reify is opened in a new browser window pointing at the saved project/screen.

---
## Method: ReportBuilder.addComponentViaAI

### Description
Adds a component to the report based on a natural language description.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| prompt | [String](#type-string) | false | — | description of the component to create |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired when component is added |

---
## Method: ReportBuilder.setReportQuery

### Description
Sets report-level query configuration including criteria, groupBy, and summaryFunctions. This affects all data-bound components in the report.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsRequestProps | [DSRequest Properties](#type-dsrequest-properties) | false | — | query configuration |

---
## Method: ReportBuilder.publishReport

### Description
Publishes the current report to a shareable URL via [Reify.publishScreen](Reify.md#classmethod-reifypublishscreen). The report's EditContext is serialized, saved as a Reify screen, added to the [ReportBuilder.reifyProjectName](#attr-reportbuilderreifyprojectname) project, and a share record is written to `isc_sharedProjects`. On success a dialog displays the copyable share URL.

This reuses the same Reify infrastructure (`projectRunner.jsp`) that [Reify.publishProject](#method-reifypublishproject) uses, so the published report is a real Reify screen that can also be opened in Reify for further editing.

---
