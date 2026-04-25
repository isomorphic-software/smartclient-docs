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
## Attr: ReportBuilder.editArea

### Description
Right panel containing the EditPane and optional PropertySheet.

**Flags**: R

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
Layout containing the AI prompt form for natural language report creation.

**Flags**: R

---
## Attr: ReportBuilder.reportSaved

### Description
Notification fired after a report is successfully saved.

Signature: `reportSaved(report)` where `report` is the saved report record (`Object`).

**Flags**: IRW

---
## Attr: ReportBuilder.defaultExportFormat

### Description
Default format for report export.

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
DataSources available for report building. Can be an array of DataSource instances or DataSource IDs. If not specified, uses isc.AI.getDataSourceNames() to discover available DataSources.

**Flags**: IRW

---
## Attr: ReportBuilder.exportFormats

### Description
Available export formats for reports.

**Flags**: IRW

---
## Attr: ReportBuilder.aiPromptForm

### Description
Form for entering AI prompts to generate report components.

**Flags**: R

---
## Attr: ReportBuilder.defaultPortalColumns

### Description
Initial number of columns in the PortalLayout. Additional columns are created automatically when dragging components to the right edge, and empty columns are removed automatically.

**Flags**: IRW

---
## Attr: ReportBuilder.parameterFields

### Description
Field definitions for report-level parameters. These appear in a parameter form above the report and filter all data-bound components.

**Flags**: IRW

---
## Attr: ReportBuilder.exportMenu

### Description
Menu for selecting export format.

**Flags**: R

---
## Attr: ReportBuilder.componentCreated

### Description
Notification fired after a component is added to the report.

Signature: `componentCreated(editNode, paletteNode)` where:

*   `editNode` - the created [EditNode](../reference.md#object-editnode)
*   `paletteNode` - the source [PaletteNode](../reference.md#object-palettenode)

**Flags**: IRW

---
## Attr: ReportBuilder.componentPalette

### Description
Palette containing available component types. Data Views are standalone components that use the DataSource picker. Uses ListPalette so that setDefaultPalette works correctly and the framework handles drop positioning automatically.

**Flags**: R

---
## Attr: ReportBuilder.toolbar

### Description
ToolStrip providing report-level actions: Save, Load, Export, New, etc.

**Flags**: R

---
## Attr: ReportBuilder.mainLayout

### Description
Main horizontal layout containing the palette panel and edit area.

**Flags**: R

---
## Attr: ReportBuilder.reportSaveDialog

### Description
Dialog for saving reports with title and description.

**Flags**: R

---
## Attr: ReportBuilder.reportDataSource

### Description
DataSource for persisting saved reports. If not specified, reports can only be saved to local storage or exported.

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
## Method: ReportBuilder.setReportDefinition

### Description
Loads a serialized report definition.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| definition | [String](#type-string) | false | — | serialized report XML |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback fired after load completes |

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
Returns all component EditNodes in the report.

### Returns

`[Array of EditNode](#type-array-of-editnode)` — array of component EditNodes

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
