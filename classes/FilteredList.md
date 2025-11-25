# FilteredList Documentation

[← Back to API Index](../main.md)

---

## Class: FilteredList

*Inherits from:* [ResultSet](ResultSet.md#class-resultset)

### Description
A subclass of [ResultSet](ResultSet.md#class-resultset) designed to provide a synchronously filterable List interface for an array of data.

Developers should set [FilteredList.allRows](#attr-filteredlistallrows) to the full set of data objects, and use [criteria](ResultSet.md#attr-resultsetcriteria) to the apply criteria to the data set. Standard List APIs such as [List.get](List.md#method-listget), [List.getLength](List.md#method-listgetlength), [List.getRange](List.md#method-listgetrange), etc will then allow access to a filtered subset of this data.

The [FilteredList.dataSource](#attr-filteredlistdatasource) attribute may be used to specify the format of records to be stored within this list, but this is not required. If no DataSource is explicitly specified, filteredList will automatically generate its own DataSource with [dropUnknownCriteria](DataSource.md#attr-datasourcedropunknowncriteria) set to false.

---
## Attr: FilteredList.dataSource

### Description
Optional dataSource to specifying field names and types for records within this List. Note that since a full data set should be provided to the list via [FilteredList.allRows](#attr-filteredlistallrows), this filteredList will not issue fetch requests against this DataSource.

If no DataSource was explicitly specified, filteredList will automatically generate its own DataSource with [dropUnknownCriteria](DataSource.md#attr-datasourcedropunknowncriteria) set to false.

**Flags**: IR

---
## Attr: FilteredList.allRows

### Description
Complete set of records for this filteredList. Sorting and filtering of this list will occur synchronously on the client.

**Flags**: IRA

---
## Attr: FilteredList.modifiable

### Description
When true, allows the ResultSet to be modified by list APIs [List.addAt](List.md#method-listaddat), [List.set](List.md#method-listset), and [List.removeAt](List.md#method-listremoveat). Only applies to [fetchMode](ResultSet.md#attr-resultsetfetchmode):"local" ResultSets, since in all other cases, such modifications would break the consistency of server and client row numbering needed for data paging, and also create some issues with automatic cache synchronization. See the "Modifying ResultSets" subtopic in the [ResultSet Overview](ResultSet.md#class-resultset) for the alternative approach of updating the [DataSource](DataSource.md#class-datasource).

One known case where modification can be useful is when an array has been passed to [ListGrid.setData](ListGrid_2.md#method-listgridsetdata) for a ListGrid with [ListGrid.filterLocalData](ListGrid_1.md#attr-listgridfilterlocaldata):true. If the data is filtered using the [filterEditor](ListGrid_1.md#attr-listgridshowfiltereditor), then a new local ResultSet will be created as [data](ListGrid_1.md#attr-listgriddata) to reflect the filtering.

### Groups

- cacheSync

### See Also

- [DataSource.addData](DataSource.md#method-datasourceadddata)
- [DataSource.removeData](DataSource.md#method-datasourceremovedata)
- [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches)

**Flags**: IRW

---
## Method: FilteredList.setAllRows

### Description
Updates [FilteredList.allRows](#attr-filteredlistallrows) at run time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| allRows | [Array of Records](#type-array-of-records) | false | — | New set of unfiltered cache data |

---
## Method: FilteredList.invalidateCache

### Description
Invoking invalidateCache() will have no effect on a filteredList. To drop the _allRows_ cache of data, consider passing an empty array to [FilteredList.setAllRows](#method-filteredlistsetallrows).

---
