# SetFilterItem Documentation

[← Back to API Index](../main.md)

---

## Class: SetFilterItem

*Inherits from:* [MultiPickerItem](MultiPickerItem.md#class-multipickeritem)

### Description
Specialized [MultiPickerItem](MultiPickerItem.md#class-multipickeritem) used for generating search criteria in the [FilterEditor](ListGrid_1.md#attr-listgridfiltereditor) and in SearchForms.

SetFilterItem generates [inSet and notInSet](../main.md#type-operatorid) filter criteria from a set of possible values, which can be provided via an explicit [valueMap](FormItem.md#attr-formitemvaluemap) or [optionDataSource](MultiPickerItem.md#attr-multipickeritemoptiondatasource), or can be derived from the [target databound component](#attr-setfilteritemfiltertargetcomponent) or a [list of records](#attr-setfilteritemsourcelist).

In particular, when attached to a databound component such as a ListGrid, SetFilterItem can provide "Excel-style filtering", allowing the user to pick from amongst whatever values are present in the dataset.

For large datasets, SetFilterItem will also intelligently use locally cached data when possible, deriving its set of options from loaded data without the need for an extra dataSource fetch. Specifically, when [all matching records](ResultSet.md#method-resultsetallmatchingrowscached) are loaded in the [SetFilterItem.filterTargetComponent](#attr-setfilteritemfiltertargetcomponent), the options are derived from already loaded data. If the set of data is incomplete (due to [data paging](ResultSet.md#attr-resultsetfetchmode)), the SetFilterItem will derive options from its optionDataSource.

Note that [SetFilterItem.deriveUniqueValues](#attr-setfilteritemderiveuniquevalues) defaults to `true` for setFilterItems.

When a SetFilterItem is used as a [ListGrid filterEditor](ListGridField.md#attr-listgridfieldfiltereditortype), the filterTargetComponent will automatically be set to the grid being filtered.

The item's picker-component can be customized via settings such as [sortField](MultiPickerItem.md#attr-multipickeritemsortfield), or by configuring [auto-children](../main.md#type-autochild) like the [search-form](MultiPickerItem.md#attr-multipickeritemfilterform), the [main pickList-grid](MultiPickerItem.md#attr-multipickeritempicklist) or the separate list of [selected values](MultiPickerItem.md#attr-multipickeritemselectionlist). You can use [MultiPickerItem.optionFilterContext](MultiPickerItem.md#attr-multipickeritemoptionfiltercontext) to apply custom `requestProperties` to fetches from the main `pickList` grid.

---
## Attr: SetFilterItem.expandedPickListFields

### Description
If [SetFilterItem.canExpand](#attr-setfilteritemcanexpand) is true, this is the list of fields to display in the [PickList](../main_2.md#interface-picklist) or [pickTree](MultiPickerItem.md#attr-multipickeritempicktree) when the picker is expanded

**Flags**: IR

---
## Attr: SetFilterItem.toggleUseUnselectedValuesOnSelectAll

### Description
Should this item toggle between tracking selected options and using them to generate "inSet" criteria and unselected options and using them to generate "notInSet" criteria when the user clicks the [MultiPickerItem.selectAllButton](MultiPickerItem.md#attr-multipickeritemselectallbutton) and [MultiPickerItem.deselectAllButton](MultiPickerItem.md#attr-multipickeritemdeselectallbutton) on an unfiltered list of options.

See [SetFilterItem.useUnselectedValues](#attr-setfilteritemuseunselectedvalues) for more detail

**Flags**: IRA

---
## Attr: SetFilterItem.selectionStyle

### Description
selectionStyle:"shuttle" is not supported for SetFilterItem

**Flags**: IR

---
## Attr: SetFilterItem.pickListFields

### Description
Optional list of fields for the [MultiPickerItem.pickList](MultiPickerItem.md#attr-multipickeritempicklist). This property may be used to customize the appearance of the field / fields in the pickList.

If not explicitly specified, pick list fields will be generated automatically to show the display field (or value field if there is no display field) for each option.

Note that if [SetFilterItem.canExpand](#attr-setfilteritemcanexpand) is true, developers should use [SetFilterItem.expandedPickListFields](#attr-setfilteritemexpandedpicklistfields) to specify the set of fields to display in the expanded view.

**Flags**: IR

---
## Attr: SetFilterItem.sourceList

### Description
If specified, this picker will derive its set of options from this list of records.

Note that if the `sourceList` list is a ResultSet that has not got a complete [cache of data](ResultSet.md#method-resultsetallmatchingrowscached) for its criteria, options will be derived by performing a fetch against the resultSet's dataSource.

**Flags**: IRA

---
## Attr: SetFilterItem.filterTargetComponent

### Description
Target component for which this SetFilterItem is generating criteria. By default the [SetFilterItem.sourceList](#attr-setfilteritemsourcelist) will be the [data object](ListGrid_1.md#attr-listgriddata) for the target component, and the option dataSource, option criteria, option fetch operation and so on will be derived from the target component's configuration.

For a setFilterItem embedded in a [filter editor](ListGrid_1.md#attr-listgridshowfiltereditor), this will be the target listGrid.

**Flags**: IR

---
## Attr: SetFilterItem.unselectedOperator

### Description
Operator for the criteria generated by this item when [SetFilterItem.useUnselectedValues](#attr-setfilteritemuseunselectedvalues) is true.

**Flags**: IRA

---
## Attr: SetFilterItem.selectedOperator

### Description
Operator for the criteria generated by this item when [SetFilterItem.useUnselectedValues](#attr-setfilteritemuseunselectedvalues) is false.

**Flags**: IRA

---
## Attr: SetFilterItem.deriveUniqueValues

### Description
If this MultiPickerItem is deriving its options from a dataSource, should it ensure unique field values by [grouping by](DSRequest.md#attr-dsrequestgroupby) the value field for this item? This is not necessary if the target dataSource value field is already unique - for example if this is the primaryKey field for a dataSource.

Note that for MultiPickerItems with `deriveUniqueValues:true`, any [SetFilterItem.expandedPickListFields](#attr-setfilteritemexpandedpicklistfields) to be displayed in the [expanded view](MultiPickerItem.md#attr-multipickeritemcanexpand) will not be able to display meaningful values unless a [summaryFunction](DSRequest.md#attr-dsrequestsummaryfunctions) is supplied to produce aggregated values from the grouped data. This may be achieved by specifying summaryFunctions directly on the [optionFilterContext](MultiPickerItem.md#attr-multipickeritemoptionfiltercontext), or on the [operationBinding](DataSource.md#attr-datasourceoperationbindings) for the [fetch operation](MultiPickerItem.md#attr-multipickeritemoptionoperationid).

**Flags**: IRA

---
## Attr: SetFilterItem.useUnselectedValues

### Description
The SetFilterItem has the capability to treat its set of options as selected by default, and explicitly track the options a user has unselected, or treat them as unselected by default and explicitly track the user-selected objects. This attribute denotes whether the item is currently tracking explicitly selected or unselected values.

While tracking selected values, this item will generate [inSet](#attr-setfilteritemselectedoperator) criteria. While tracking unselected values, it will generate [notInSet](#attr-setfilteritemunselectedoperator) criteria.

If [SetFilterItem.toggleUseUnselectedValuesOnSelectAll](#attr-setfilteritemtoggleuseunselectedvaluesonselectall) is true, if the current set of options is unfiltered, the [MultiPickerItem.selectAllButton](MultiPickerItem.md#attr-multipickeritemselectallbutton) and [MultiPickerItem.deselectAllButton](MultiPickerItem.md#attr-multipickeritemdeselectallbutton) will clear any current value and toggle useUnselectedValues - effectively switching between tracking inclusive (inSet) values and exclusive (notInSet) values.

**Flags**: IRW

---
## Attr: SetFilterItem.canExpand

### Description
Should we show an [MultiPickerItem.expansionIcon](MultiPickerItem.md#attr-multipickeritemexpansionicon) expand button allowing the user to show an expanded view of the [MultiPickerItem.pickList](MultiPickerItem.md#attr-multipickeritempicklist) with multiple fields.

`canExpand` only applies to MultiPickerItems with selectionStyle set to "pickList" or "pickTree" and an explicitly specified set of [MultiPickerItem.expandedPickListFields](MultiPickerItem.md#attr-multipickeritemexpandedpicklistfields) to display within the expanded view.

**Flags**: IR

---
## Attr: SetFilterItem.defaultUseUnselectedValues

### Description
Should this item track unselected or selected values by default?

If [SetFilterItem.toggleUseUnselectedValuesOnSelectAll](#attr-setfilteritemtoggleuseunselectedvaluesonselectall), for setFilterItems with no current criteria (I.E. no explicitly selected or unselected values), this property will be evaluated when the pickList is shown and [SetFilterItem.useUnselectedValues](#attr-setfilteritemuseunselectedvalues) will be set to match this value. This causes the options in the pickList to always show up checked (or unchecked) by default, matching user expectations of what an "empty" filter represents.

May be set to null, in which case useUnselectedValues will not be modified when the pickList is shown for an empty SetFilterItem

**Flags**: IRA

---
## Method: SetFilterItem.setUseUnselectedValues

### Description
Clear any current value for this item and dynamically update [SetFilterItem.useUnselectedValues](#attr-setfilteritemuseunselectedvalues).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| useUnselectedValues | [boolean](../main.md#type-boolean) | false | — | new value for useUnselectedValues |

---
