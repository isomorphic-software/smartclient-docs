# Data Context and Shared Criteria

[← Back to API Index](../reference.md)

---

## KB Topic: Data Context and Shared Criteria

### Description
A [Canvas.dataContext](../classes/Canvas.md#attr-canvasdatacontext) binds the data-bound components beneath a [Canvas](../classes/Canvas.md#class-canvas) to a set of records from one place. It maps [DataSource](../classes/DataSource_1.md#class-datasource) IDs to specific [Records](../reference.md#object-record); any [DataBoundComponent](../reference.md#interface-databoundcomponent) under the Canvas that has a DataSource but no data of its own populates from the matching entry, binding to the nearest enclosing Canvas that carries one. It is how a screen is handed "the records it is about": give it `{Order: anOrderRecord}` and the order form, detail viewers and related line-item grids beneath it fill in together, with no per-component fetch. See [Canvas.autoPopulateData](../classes/Canvas.md#attr-canvasautopopulatedata) for the rules - a singular component (a [DynamicForm](../classes/DynamicForm.md#class-dynamicform) or [DetailViewer](../classes/DetailViewer.md#class-detailviewer)) shows or edits the record; a list component (a [ListGrid](../classes/ListGrid_1.md#class-listgrid)) uses non-key fields as criteria, and a primary key against a related DataSource pulls related records as [ListGrid.fetchRelatedData](../classes/ListGrid_2.md#method-listgridfetchrelateddata) would, such as an order's line items.

A dataContext's DataSources are also exposed to [rule context](#rulescope) as `dataContext.`<DataSourceID>``, so visibility, validation and dynamic criteria can react to "the current Customer" without a component fetching it; and [Canvas.testDataContext](../classes/Canvas.md#attr-canvastestdatacontext) supplies sample records when none is set, so a screen can be built and tested in isolation.

A dataContext may also carry a reserved `sharedCriteria` key: a shared-criteria bus that every subscribing component folds into its fetch, contributed through [Canvas.setDataContextCriteria](../classes/Canvas.md#method-canvassetdatacontextcriteria) and carrying the envelope in [DataContextCriteriaSettings](#object-datacontextcriteriasettings). Two features publish onto it:

*   **Filter sharing** - authored filter controls and components that share their own criteria ([Canvas.shareCriteria](../classes/Canvas.md#attr-canvassharecriteria), consumed per [Canvas.useDataContextCriteria](../classes/Canvas.md#attr-canvasusedatacontextcriteria); a [Slicer](../classes/Slicer.md#class-slicer) is the common example): "filter"-type contributions, part of the saved screen.
*   **Selection sharing** - a selection in one component narrowing others ([selectionSharing](#kb-topic-selectionsharing)): "dataSelection"-type contributions, interaction state that is never serialized.

### Related

- [Canvas.setDataContext](../classes/Canvas.md#method-canvassetdatacontext)
- [Canvas.setDataContextCriteria](../classes/Canvas.md#method-canvassetdatacontextcriteria)
- [Canvas.getDataContextCriteria](../classes/Canvas.md#method-canvasgetdatacontextcriteria)
- [Canvas.handleDataContextCriteria](../classes/Canvas.md#method-canvashandledatacontextcriteria)
- [Canvas.dataContextCriteriaChanged](../classes/Canvas.md#method-canvasdatacontextcriteriachanged)
- [Canvas.dataContextChanged](../classes/Canvas.md#method-canvasdatacontextchanged)
- [ScreenLoader.setDataContextBinding](../classes/ScreenLoader.md#method-screenloadersetdatacontextbinding)
- [ScreenLoader.dataContextChanged](../classes/ScreenLoader.md#method-screenloaderdatacontextchanged)
- [Canvas.dataContext](../classes/Canvas.md#attr-canvasdatacontext)
- [Canvas.testDataContext](../classes/Canvas.md#attr-canvastestdatacontext)
- [DataContext.sharedCriteria](../classes/DataContext.md#attr-datacontextsharedcriteria)
- [Canvas.useDataContextCriteria](../classes/Canvas.md#attr-canvasusedatacontextcriteria)
- [Canvas.autoPopulateData](../classes/Canvas.md#attr-canvasautopopulatedata)
- [Canvas.shareCriteria](../classes/Canvas.md#attr-canvassharecriteria)
- [LoadProjectSettings.dataContext](../classes/LoadProjectSettings.md#attr-loadprojectsettingsdatacontext)
- [CreateScreenSettings.dataContext](../classes/CreateScreenSettings.md#attr-createscreensettingsdatacontext)
- [ScreenLoader.dataContextBinding](../classes/ScreenLoader.md#attr-screenloaderdatacontextbinding)

---
