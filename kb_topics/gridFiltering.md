# Grid Filtering Overview

[← Back to API Index](../reference.md)

---

## KB Topic: Grid Filtering Overview

### Description
This overview discusses various ways that [search criteria](../reference_2.md#type-criteria) can be applied to a [grid](../classes/ListGrid_1.md#class-listgrid) to filter the data being displayed.

Typically, there are two types of criteria that affect how a grid matches data:

*   Implicit criteria - hidden criteria, applied by the developer, to the [grid](../classes/ListGrid_1.md#attr-listgridimplicitcriteria) or its [dataSource](../classes/DataSource.md#attr-datasourceimplicitcriteria), and never made available to users
*   Explicit criteria - public criteria, which may be applied by the developer or entered by the user - this criteria may be displayed to and modified by the user at runtime in various ways

A grid may have both implicit criteria, and explicit criteria that may come from multiple sources. When data is fetched, the implicit-criteria and any sources of [explicit criteria](../classes/ListGrid_2.md#method-listgridgetcriteria) are [combined](../classes/DataSource.md#classmethod-datasourcecombinecriteria) and used to match records.

Note, however, that attempts to fetch with more restrictive criteria may not result in a server-trip, because [ResultSet](../classes/ResultSet.md#class-resultset)s implement local filtering adaptively and may not require a server-trip if a filter can be achieved from local caches.

#### Initial Filter Criteria
You can provide an initial filter for a grid by setting [implicit criteria](../classes/ListGrid_1.md#attr-listgridimplicitcriteria), which is never shown to the user, or [initial criteria](../classes/ListGrid_1.md#attr-listgridinitialcriteria), which may be shown for editing in the grid's builtin [filter-row](../classes/ListGrid_1.md#attr-listgridshowfiltereditor). You can also provide both types, if only some parts of the criteria should be public.
#### Filter Row Criteria
Grids provide a [filter-row](../classes/ListGrid_1.md#attr-listgridfiltereditor) that allows users to apply search-values on a per-field basis. When [ListGrid.allowFilterOperators](../classes/ListGrid_1.md#attr-listgridallowfilteroperators) is true, the default, users can modify the [search operator](../reference.md#object-operator) assigned to a given field via the grid's [header context-menu](../classes/ListGrid_1.md#attr-listgridheadercontextmenu), allowing for more complex matching. If the selected operator is not the field's [default operator](../classes/ListGridField.md#attr-listgridfieldfilteroperator), or if [ListGrid.alwaysShowOperatorIcon](../classes/ListGrid_1.md#attr-listgridalwaysshowoperatoricon) is true, the current operator is indicated in a small icon in each filter-field.

Developers can interact with a field's search operator with [ListGrid.getFieldSearchOperator](../classes/ListGrid_2.md#method-listgridgetfieldsearchoperator), [ListGrid.setFieldSearchOperator](../classes/ListGrid_2.md#method-listgridsetfieldsearchoperator) and [ListGrid.clearFieldSearchOperator](../classes/ListGrid_2.md#method-listgridclearfieldsearchoperator).

Criteria in the filter-row reflects current public criteria that [can be edited](../classes/FormItem.md#method-formitemcaneditcriterion). Developers can retrieve this criteria with [ListGrid.getFilterEditorCriteria](../classes/ListGrid_2.md#method-listgridgetfiltereditorcriteria) and set it with [ListGrid.setFilterEditorCriteria](../classes/ListGrid_2.md#method-listgridsetfiltereditorcriteria). When the filter-row is showing, Calls to APIs such as [ListGrid.setCriteria](../classes/ListGrid_2.md#method-listgridsetcriteria) or [ListGrid.fetchData](../classes/ListGrid_2.md#method-listgridfetchdata) will apply criteria to the filter-row, if the editors there allow it. Any criteria applied by these methods, that cannot be edited by the associated field's filter-editor, are still applied to fetches and will be returned by calls to [ListGrid.getCriteria](../classes/ListGrid_2.md#method-listgridgetcriteria) or [ListGrid.getFilterEditorCriteria](../classes/ListGrid_2.md#method-listgridgetfiltereditorcriteria), but are not shown to the user for editing.

Developers may specify a field's [filterEditor-type](../classes/ListGridField.md#attr-listgridfieldfiltereditortype), and this can be a custom [FormItem](../classes/FormItem.md#class-formitem) class that uses [getCriterion()](../classes/FormItem.md#method-formitemgetcriterion), [setCriterion()](../classes/FormItem.md#method-formitemsetcriterion) and [canEditCriterion()](../classes/FormItem.md#method-formitemcaneditcriterion) to manage the criteria it works with.

For more complicated cases or more control, developers can implement [ListGrid.filterEditorSubmit](../classes/ListGrid_2.md#method-listgridfiltereditorsubmit).

Criteria from the filter-row is combined with other sources of criteria when data is fetched.

#### External Criteria
If you have external logic, or a [form](../classes/SearchForm.md#class-searchform) outside of the grid, that produces criteria, you can apply the criteria by passing it to [fetchData](../classes/ListGrid_2.md#method-listgridfetchdata) or [filterData](../classes/ListGrid_2.md#method-listgridfilterdata). The primary difference between these two APIs is that `filterData` applies a [DSRequest.textMatchStyle](../classes/DSRequest.md#attr-dsrequesttextmatchstyle) of _substring_, so that records are matched by case-insensitive substring comparison.

If you have the `FilterEditor` showing, these external criteria will be appear in the filterEditor, where supported. Developers can apply additional external criteria without that effect by passing them to [DataBoundComponent.setImplicitCriteria](../classes/DataBoundComponent.md#method-databoundcomponentsetimplicitcriteria), or by setting [ListGrid.searchForm](../classes/ListGrid_1.md#attr-listgridsearchform) to the external criteria form.

If you need more power or variance than the filter-row provides, you can set [ListGrid.allowFilterWindow](../classes/ListGrid_1.md#attr-listgridallowfilterwindow) to show a full-blown [FilterBuilder](../classes/FilterBuilder.md#class-filterbuilder), to construct more complex criteria that can also include logical operators like _or_.

All sources of criteria are combined to match records when data is fetched.

#### Saving Criteria
Grid criteria can be saved and restored with [view-state](../classes/ListGrid_2.md#method-listgridgetviewstate) and via the [SavedSearches](../classes/SavedSearches.md#class-savedsearches) feature, which is turned on by default.

---
