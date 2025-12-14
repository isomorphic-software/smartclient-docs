# ResultSet Documentation

[← Back to API Index](../reference.md)

---

## Class: ResultSet

### Description
ResultSets are an implementation of the [List](../reference.md#interface-list) interface that automatically fetches DataSource records when items are requested from the List. ResultSets provide robust, customizable, high-performance cache management for ListGrids and other built-in SmartClient components, and can be used as cache managers by custom components.

ResultSets manage data paging, that is, loading records in batches as the user navigates the data set. A ResultSet will switch to using client-side sorting and filtering when possible to improve responsiveness and reduce server load. ResultSets also participate in automatic cache synchronization, observing operations on DataSources and automatically updating their caches.

**Creation**

A ResultSet can be passed to any component that expects a List, and the List APIs can be called directly on the ResultSet as long as the caller is able to deal with asynchronous loading; see [ResultSet.getRange](#method-resultsetgetrange).

Generally ResultSets do not need to be created directly, but are created by DataBound components as an automatic consequence of calling [DataBound Component Methods](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods). For example, the [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata) causes [ListGrid.data](ListGrid_1.md#attr-listgriddata) to become an automatically created `ResultSet` object. Automatically created ResultSets can be customized via properties on ListGrids such as [ListGrid.dataPageSize](ListGrid_1.md#attr-listgriddatapagesize) and [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). All ResultSets for a given DataSource may also be customized via setting [DataSource.resultSetClass](DataSource.md#attr-datasourceresultsetclass) to the name of a ResultSet [subclass](isc.md#staticmethod-iscdefineclass) in which [defaults have been changed](Class.md#classmethod-classaddproperties).

A ResultSet defaults to using data paging, setting [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow) and [DSRequest.endRow](DSRequest.md#attr-dsrequestendrow) in issued dsRequests. Server code may always return more rows than the ResultSet requests and the ResultSet will correctly integrate those rows based on [DSResponse.startRow](DSResponse.md#attr-dsresponsestartrow)/[endRow](DSResponse.md#attr-dsresponseendrow). Hence the server can always avoid paging mode by simply returning all matching rows.

A ResultSet can be created directly with just the ID of a [DataSource](DataSource.md#class-datasource):

```
     isc.ResultSet.create({
         dataSource : "dataSourceID"
     })
 
```

Directly created ResultSets are typically used by custom components, or as a means of managing datasets that will be used by several components.

When created directly rather than via a dataBoundComponent, a newly created ResultSet will not issue it's first "fetch" [DSRequest](../reference.md#object-dsrequest) until data is accessed (for example, via [get()](#method-resultsetget)).

**Paging and total dataset length**

When using data paging, the server communicates the total number of records that match the current search criteria by setting [DSResponse.totalRows](DSResponse.md#attr-dsresponsetotalrows). The ResultSet will then return this number from [getLength()](#method-resultsetgetlength), and ListGrids and other components will show a scrollbar that allows the user to jump to the end of the dataset directly.

However, the ResultSet does not require that the server calculate the true length of the dataset, which can be costly for an extremely large, searchable dataset. Instead, the server _may_ advertise a `totalRows` value that is one page larger than the last row loaded. This results in a UI sometimes called "progressive loading", where the user may load more rows by scrolling past the end of the currently loaded rows, but is not allowed to skip to the end of the dataset.

The SmartClient server offers built in support for progressive loading at the [dataSource](DataSource.md#attr-datasourceprogressiveloading), [operationBinding](OperationBinding.md#attr-operationbindingprogressiveloading) and [request](DSRequest.md#attr-dsrequestprogressiveloading) level for SQL-backed dataSources. Setting [ResultSet.progressiveLoading](#attr-resultsetprogressiveloading) or [DataBoundComponent.progressiveLoading](DataBoundComponent.md#attr-databoundcomponentprogressiveloading) to true will also enable this feature where available.

Where available, progressive loading will also be enabled automatically for very large data sets if a [DataSource.progressiveLoadingThreshold](DataSource.md#attr-datasourceprogressiveloadingthreshold) is specified.

Note that the SmartClient server is not a requirement for progressive loading - any DataSource implementation can enable progressive loading by simply populating the [DSResponse.totalRows](DSResponse.md#attr-dsresponsetotalrows) property with an appropriate value. We recommend the [DSResponse.progressiveLoading](DSResponse.md#attr-dsresponseprogressiveloading) attribute be set to true as well - this allows client side logic to treat the reported totalRows value specially if necessary.

No client-side settings are required to enable this mode - it is entirely server-driven. However, it is usually coupled with [disabling sorting](ListGrid_1.md#attr-listgridcansort), since server-side sorting would also force the server to traverse the entire dataset.

**Client-side Sorting and Filtering**

If a ResultSet obtains a full cache for the current set of filter criteria, it will automatically switch to client-side sorting, and will also use client-side filtering if the filter criteria are later changed but appear to be _more restrictive_ than the criteria in use when the ResultSet obtained a full cache.

The [useClientSorting](#attr-resultsetuseclientsorting) and [useClientFiltering](#attr-resultsetuseclientfiltering) flags can be used to disable client-side sorting and filtering respectively if these behaviors don't match server-based sorting and filtering. However, because client-side sorting and filtering radically improve responsiveness and reduce server load, it is better to customize the ResultSet so that it can match server-side sorting and filtering behaviors.

Sorting behavior is primarily customized via the "sort normalizer" passed to [ResultSet.sortByProperty](#method-resultsetsortbyproperty), either via direct calls on a standalone ResultSet, or via [ListGridField.sortNormalizer](ListGridField.md#method-listgridfieldsortnormalizer) for a ListGrid-managed ResultSet.

By default, client-side filtering interprets the [criteria](../reference_2.md#type-criteria) passed to [setCriteria()](#method-resultsetsetcriteria) as a set of field values that records must match (similarly to the built-in SQL/Hibernate connectors built into the SmartClient Server). Custom client-side filtering logic can be implemented by overriding [applyFilter()](#method-resultsetapplyfilter). Overriding [compareCriteria()](#method-resultsetcomparecriteria) allows you to control when the ResultSet uses client-side vs server-side filtering, and the ResultSet has two default [criteria policies](#attr-resultsetcriteriapolicy) built-in.

**Modifying ResultSets**

Records cannot be directly added or removed from a ResultSet via [List](../reference.md#interface-list) APIs such as [removeAt()](List.md#method-listremoveat), unless it always filters locally, since this would break the consistency of server and client row numbering needed for data paging, and also create some issues with automatic cache synchronization. Set [modifiable](#attr-resultsetmodifiable) to enable the [List](../reference.md#interface-list) modification APIs on a [fetchMode](#attr-resultsetfetchmode):"local" ResultSet. Note that the special [FilteredList](FilteredList.md#class-filteredlist) class sets this property to allow developers to modify its data.

Use [DataSource.addData](DataSource.md#method-datasourceadddata)/[removeData()](DataSource.md#method-datasourceremovedata) to add/remove rows from the [DataSource](DataSource.md#class-datasource), and the ResultSet will reflect the changes automatically. Alternatively, the [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches) method may be called to only update local caches of the DataSource in question, without generating any server traffic.

To create a locally modifiable cache of Records from a DataSource, you can use [DataSource.fetchData](DataSource.md#method-datasourcefetchdata) to retrieve a List of Records which can be modified directly, or you can create a client-only [DataSource](DataSource.md#class-datasource) from the retrieved data to share a modifiable cache between several DataBoundComponents.

**Updates and Automatic Cache Synchronization**

Once a ResultSet has retrieved data or has been initialized with data, the ResultSet will observe any successful "update", "add" or "remove" dsRequests against their DataSource, regardless of the component that initiated them. A ResultSet with a full cache for the current filter criteria will integrate updates into the cache automatically.

Updated rows that no longer match the current filter criteria will be removed automatically. To prevent this, you can set [ResultSet.neverDropUpdatedRows](#attr-resultsetneverdropupdatedrows). Added rows will similarly be added to the cache only if they match current filter criteria.

Note that the client-side filtering described above is also used to determine whether updated or added rows should be in the cache. If any aspect of automated cache update is ever incorrect, [dropCacheOnUpdate](#attr-resultsetdropcacheonupdate) can be set for the ResultSet or [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache) can be set for an individual dsResponse.

If automatic cache synchronization isn't working, troubleshoot the problem using the steps suggested [in the FAQ](http://forums.smartclient.com/showthread.php?t=8159#aGrid).

Regarding [operationIds](OperationBinding.md#attr-operationbindingoperationid) and how they affect caching, take into account that cache sync is based on the fetch used - any add or update operation uses a fetch to retrieve updated data, and the operationId of that fetch can be set via [cacheSyncOperation](OperationBinding.md#attr-operationbindingcachesyncoperation). If the operationId of the cache is different from the operationId of the cache update data, it won't be used to update the cache, since the fields included and other aspects of the data are allowed to be different across different operationIds. This allows to maintain distinct caches on a per component basis, so when two components are using separate operationIds they are assumed to have distinct caches, because updates performed with one operationId will not affect the cache obtained via another operationId. Also, take into account that operationId must be unique per DataSource, across all operationTypes for that DataSource.

**Data Paging with partial cache**

When in paging mode with a partial cache, a ResultSet relies on server side sorting, setting [DSRequest.sortBy](DSRequest.md#attr-dsrequestsortby) to the current sort field and direction. In order for the cache to remain coherent, row numbering must continue to agree between server and client as new fetches are issued, otherwise, duplicate rows or missing rows may occur.

If concurrent modifications by other users are allowed, generally the server should set [DSResponse.invalidateCache](DSResponse.md#attr-dsresponseinvalidatecache) to clear the cache when concurrent modification is detected.

In paging mode with a partial cache, any successful "update" or "add" operation may cause client and server row numbering to become out of sync. This happens because the update may affect the sort order, and client and server cannot be guaranteed to match for sets of records that have equivalent values for the sort field.

For this reason, after an "add" or "update" operation with a partial cache, the ResultSet will automatically mark cache for invalidation the next time a fetch operation is performed. Alternatively, if [ResultSet.updatePartialCache](#attr-resultsetupdatepartialcache) is set to false, the ResultSet will simply invalidate cache immediately in this circumstance.

### See Also

- [DataBoundComponent](../reference.md#interface-databoundcomponent)
- [dataBoundComponentMethods](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods)
- [DataSource.resultSetClass](DataSource.md#attr-datasourceresultsetclass)
- [ResultSet.getRange](#method-resultsetgetrange)

---
## Attr: ResultSet.requestProperties

### Description
Allows to set a DSRequest properties to this ResulSet.

**Flags**: IR

---
## Attr: ResultSet.initialData

### Description
Initial set of data for the ResultSet.

This data will be treated exactly as though it were the data returned from the ResultSet's first server fetch.

By default, `initialData` will be considered a complete response (all rows that match the [Criteria](../reference_2.md#type-criteria) which the ResultSet was initialized with).

Set [ResultSet.initialLength](#attr-resultsetinitiallength) to treat `initialData` as a partial response, equivalent to receiving a [DSResponse](DSResponse.md#class-dsresponse) with `startRow:0`, `endRow:initialData.length` and `totalRows:initialLength`. Normal data paging will then occur if data is requested for row indices not filled via `initialData`.

`initialData` may be provided as a "sparse" array, that is, slots may be left null indicating rows that have not been loaded. In this way you can create a ResultSet that is missing rows at the beginning of the dataset, but has loaded rows toward the end, so that you can create a component that is scrolled to a particular position of a dataset without loading rows at the beginning.

To keep the logic simple and support partial `initialData`, the data is assumed to be already sorted and filtered according to the [ResultSet.sortSpecifiers](#attr-resultsetsortspecifiers) and [ResultSet.criteria](#attr-resultsetcriteria) supplied to the ResultSet, since otherwise, for partial `initialData`, sorting or filtering would immediately cause the data to be discarded.

If `initialData` is complete and needs to be sorted or filtered, then don't pass the [ResultSet.sortSpecifiers](#attr-resultsetsortspecifiers) or [ResultSet.criteria](#attr-resultsetcriteria), respectively, when creating the ResultSet. Instead, call [ResultSet.setCriteria](#method-resultsetsetcriteria) or [ResultSet.setSort](#method-resultsetsetsort), respectively, on the instance afterwards.

### Groups

- fetching
- cacheSync

### See Also

- [ResultSet.fetchMode](#attr-resultsetfetchmode)
- [ResultSet.useClientFiltering](#attr-resultsetuseclientfiltering)

**Flags**: IA

---
## Attr: ResultSet.reapplyUnchangedLocalFilter

### Description
To avoid needless work, the ResultSet by default doesn't refilter the data when methods such as [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata) or [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata) are called with unchanged criteria. However, this property can be set true for backward compatibility to force refiltering if we're [filtering locally](#method-resultsetfilterlocaldata) and the criteria haven't changed. but are narrower than the criteria used to fetch the current cache.

Going forward, we may deprecate this property, so you should move to approach that doesn't require such notification in the case of unchanged criteria.

### See Also

- [ResultSet.willFetchData](#method-resultsetwillfetchdata)

**Flags**: IRWA

---
## Attr: ResultSet.criteria

### Description
Filter criteria used whenever records are retrieved.

Use [ResultSet.setCriteria](#method-resultsetsetcriteria) to change the criteria after initialization.

**Flags**: IRW

---
## Attr: ResultSet.resultSize

### Description
How many rows to retrieve at once.

Applicable only with `fetchMode: "paged"`. When a paged ResultSet is asked for rows that have not yet been loaded, it will fetch adjacent rows that are likely to be required soon, in batches of this size.

### Groups

- fetching

**Flags**: IRWA

---
## Attr: ResultSet.rememberDynamicProgressiveLoading

### Description
If [ResultSet.progressiveLoading](#attr-resultsetprogressiveloading) is not explicitly set, but the resultset recieves a response from the server where [DSResponse.progressiveLoading](DSResponse.md#attr-dsresponseprogressiveloading) is set to true, should subsequent requests for other rows in the same data set explicitly request progressiveLoading via [DSRequest.progressiveLoading](DSRequest.md#attr-dsrequestprogressiveloading), as long as the criteria are unchanged and the cache is not explicitly invalidated?

This property is useful for the case where the server side [DataSource.progressiveLoadingThreshold](DataSource.md#attr-datasourceprogressiveloadingthreshold) enabled progressive loading after the row-count query determined that the requested data set was very large. By explicitly [requesting progressive loading](DSRequest.md#attr-dsrequestprogressiveloading) for subsequent fetches the server is able to avoid an unnecessary and potentially expensive row-count query while returning other rows from the same data set.

### Groups

- progressiveLoading

**Flags**: IRW

---
## Attr: ResultSet.sortSpecifiers

### Description
Initial sort specifiers for a ResultSet. Use [ResultSet.setSort](#method-resultsetsetsort) and [ResultSet.getSort](#method-resultsetgetsort) to sort the data after initialization rather than attempting to read or modify this property directly.

Note: if [ResultSet.initialData](#attr-resultsetinitialdata) was specified, the data is assumed to already be sorted to match this sort configuration.

### Groups

- fetching
- cacheSync

**Flags**: IA

---
## Attr: ResultSet.modifiable

### Description
When true, allows the ResultSet to be modified by list APIs [List.addAt](List.md#method-listaddat), [List.set](List.md#method-listset), and [List.removeAt](List.md#method-listremoveat). Only applies to [fetchMode](#attr-resultsetfetchmode):"local" ResultSets, since in all other cases, such modifications would break the consistency of server and client row numbering needed for data paging, and also create some issues with automatic cache synchronization. See the "Modifying ResultSets" subtopic in the [ResultSet Overview](#class-resultset) for the alternative approach of updating the [DataSource](DataSource.md#class-datasource).

One known case where modification can be useful is when an array has been passed to [ListGrid.setData](ListGrid_2.md#method-listgridsetdata) for a ListGrid with [ListGrid.filterLocalData](ListGrid_1.md#attr-listgridfilterlocaldata):true. If the data is filtered using the [filterEditor](ListGrid_1.md#attr-listgridshowfiltereditor), then a new local ResultSet will be created as [data](ListGrid_1.md#attr-listgriddata) to reflect the filtering.

### Groups

- cacheSync

### See Also

- [DataSource.addData](DataSource.md#method-datasourceadddata)
- [DataSource.removeData](DataSource.md#method-datasourceremovedata)
- [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches)

**Flags**: IRW

---
## Attr: ResultSet.progressiveLoading

### Description
Sets [progressive loading mode](DataSource.md#attr-datasourceprogressiveloading) for this ResultSet. Any [DSRequest](../reference.md#object-dsrequest)s issued by this ResultSet will copy this setting onto the request, overriding the OperationBinding- and DataSource-level settings.

This setting is applied automatically by [DataBoundComponent](../reference.md#interface-databoundcomponent)s that have their own explicit setting for [progressiveLoading](DataBoundComponent.md#attr-databoundcomponentprogressiveloading)

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)
- [OperationBinding.progressiveLoading](OperationBinding.md#attr-operationbindingprogressiveloading)
- [DSRequest.progressiveLoading](DSRequest.md#attr-dsrequestprogressiveloading)
- [DataBoundComponent.progressiveLoading](DataBoundComponent.md#attr-databoundcomponentprogressiveloading)

**Flags**: IRW

---
## Attr: ResultSet.fetchOperation

### Description
The [operationId](DSRequest.md#attr-dsrequestoperationid) this ResultSet should use when performing fetch operations.

**Note:** if this property is not explicitly set and, for ResultSets automatically created by a component, [DataBoundComponent.fetchOperation](DataBoundComponent.md#attr-databoundcomponentfetchoperation) is also unset, a placeholder value of `<dataSourceId>`\_`<operationType>` may be reported (e.g. "supplyItem\_fetch").

**Flags**: IR

---
## Attr: ResultSet.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria), [ResultSet.setCriteria](#method-resultsetsetcriteria) etc.

**Flags**: IRW

---
## Attr: ResultSet.dropCacheOnUpdate

### Description
Whether to discard all cached rows when a modification operation (add, update, remove) occurs on the ResultSet's DataSource.

A ResultSet that has a complete cache for the current filter criteria can potentially incorporate a newly created or updated row based on the data that the server returns when a modification operation completes. However this is not always possible for ResultSets that show some types of joins, or when the server cannot easily return update data. In this case set `dropCacheOnUpdate` to cause the cache to be discarded when an update occurs.

`dropCacheOnUpdate` can be set either directly on a ResultSet, or on a DataSource in order to affect all ResultSets on that DataSource.

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultSet.useClientFiltering

### Description
Whether to filter data locally when we have a complete cache of all DataSource records for the current criteria, and the user further restricts the criteria (see [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria)).

This may need to be disabled if client-side filtering differs from server-side filtering in a way that affects functionality or is surprising.

Note that you can also prevent client-side filtering for certain fields, by setting them to ${isc.DocUtils.linkForRef('attr:DataSourceField.filterOn','filterOn: \\'serverOnly\\'')}.

This setting is distinct from `fetchMode:"local"`, which explicitly loads all available DataSource records up front and always performs all filtering on the client.

See [ResultSet.applyFilter](#method-resultsetapplyfilter) for default filtering behavior.

**NOTE:** even with useClientFiltering false, client-side filtering will be used during cache sync to determine if an updated or added row matches the current criteria. To avoid relying on client-side filtering in this case, either:  
\- avoid returning update data when the updated row doesn't match the current filter  
\- set dropCacheOnUpdate

**Flags**: IRWA

---
## Attr: ResultSet.allRows

### Description
If the complete set of records for a resultSet is available when the resultSet is created, it can be made available to the resultSet via this property at initialization time. This data will then be considered cached meaning sorting and filtering can occur on the client (no need for server fetch).

This cached data can be dropped via a call to [ResultSet.invalidateCache](#method-resultsetinvalidatecache).

See also [ResultSet.initialData](#attr-resultsetinitialdata) and [ResultSet.initialLength](#attr-resultsetinitiallength) as an alternative approach for initializing a ResultSet with a partial cache, such that data paging will occur as uncached rows are requested.

Note that developers wishing to synchronously access a filtered set of client side data may wish to consider creating a [FilteredList](FilteredList.md#class-filteredlist).

### Groups

- fetching
- cacheSync

**Flags**: IRA

---
## Attr: ResultSet.disableCacheSync

### Description
By default when the data of this ResultSet's dataSource is modified, the ResultSet will be updated to display these changes. Set this flag to true to disable this behavior.

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultSet.updateCacheFromRequest

### Description
When a successful Add, Update or Remove type operation fires on this ResultSet's dataSource, if [DSResponse.data](DSResponse.md#attr-dsresponsedata) is unset, should we integrate the submitted data values (from the request) into our data-set? This attribute will be passed to [DataSource.getUpdatedData](DataSource.md#method-datasourcegetupdateddata) as the `useDataFromRequest` parameter.

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultSet.fetchMode

### Description
Mode of fetching records from the server. If unset, will default to `"local"` if [ResultSet.allRows](#attr-resultsetallrows) is specified, otherwise `"paged"`.

### Groups

- fetching

### See Also

- [FetchMode](../reference_2.md#type-fetchmode)

**Flags**: IRA

---
## Attr: ResultSet.neverDropUpdatedRows

### Description
By default when a row is returned by the server, the current [filter\\n criteria](#method-resultsetsetcriteria) are applied to it, and it may disappear from the cache.

Set this flag to true to disable this behavior.

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultSet.criteriaPolicy

### Description
Decides under what conditions the cache should be dropped when the [Criteria](../reference_2.md#type-criteria) changes.

### See Also

- [Criteria](../reference_2.md#type-criteria)
- [DataSource.criteriaPolicy](DataSource.md#attr-datasourcecriteriapolicy)

**Flags**: IRWA

---
## Attr: ResultSet.updatePartialCache

### Description
If set to true, updated and added rows will be integrated into the client-side cache even if paging is enabled and cache is partial. If `updatePartialCache` is false, the cache will be invalidated and new data fetched.

If updatePartialCache is enabled and an "add" or "update" operation succeeds with a partial cache:

*   updated rows will remain in their current position. No attempt will be made to sort them into a new position even if the sort field was updated.
*   newly added rows will be added at either the end (first preference) or beginning of the dataset if that part of the dataset is cached and was most recently requested. If not, the new row is added at the end of the most recently requested contiguously cached range.

The cache will then be dropped the next time rows are fetched, to prevent problems with inconsistent row numbering between the server and client, which could otherwise lead to duplicate rows or rows being skipped entirely.

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultSet.dataSource

### Description
What [DataSource](DataSource.md#class-datasource) is this resultSet associated with?

### Groups

- databinding

**Flags**: IR

---
## Attr: ResultSet.fetchDelay

### Description
Delay in milliseconds before fetching rows.

When a get() or getRange() call asked for rows that haven't been loaded, the ResultSet will wait before actually triggering the request. If, during the delay, more get() or getRange() calls are made for missing rows, the final fetch to the server will reflect the most recently requested rows.

The intent of this delay is to avoid triggering many unnecessary fetches during drag-scrolling and similar user interactions.

### Groups

- fetching

**Flags**: IRWA

---
## Attr: ResultSet.initialLength

### Description
Initial value of the data set length.

To create a ResultSet with it's cache partly filled, see [ResultSet.initialData](#attr-resultsetinitialdata).

### Groups

- fetching
- cacheSync

**Flags**: IA

---
## Attr: ResultSet.alwaysRequestVisibleRows

### Description
If true, records requested only for visible area.

**Flags**: IRA

---
## Attr: ResultSet.useClientSorting

### Description
Whether to sort data locally when all records matching the current criteria have been cached.

This may need to be disabled if client-side sort order differs from server-side sort order in a way that affects functionality or is surprising.

**Flags**: IRWA

---
## ClassMethod: ResultSet.getLoadingMarker

### Description
Return the singleton marker object that is used as a placeholder for records that are being loaded from the server.

### Returns

`[String](#type-string)` — the loading marker

---
## Method: ResultSet.resort

### Description
Forcibly resort this ResultSet by the current list of [SortSpecifier](../reference.md#object-sortspecifier)s.

---
## Method: ResultSet.rangeIsLoaded

### Description
Whether the given range of rows has been loaded. Unlike getRange(), will not trigger a server fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [number](#type-number) | false | — | start position, inclusive |
| endRow | [number](#type-number) | false | — | end position, exclusive |

### Returns

`[boolean](../reference.md#type-boolean)` — true if all rows in the given range have been loaded, false if any rows in the range have not been loaded or are still in the process of being loaded

**Flags**: A

---
## Method: ResultSet.getProperty

### Description
Like [List.getProperty](List.md#method-listgetproperty). Checks only loaded rows and will not trigger a fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to look for |

### Returns

`[Array](#type-array)` — array of the values of property in each item of this list

### Groups

- iteration

---
## Method: ResultSet.filterLocalData

### Description
Derive the current filtered set of data from the cache of all matching rows.

This method is automatically called by [ResultSet.setCriteria](#method-resultsetsetcriteria) when criteria have actually changed, as well as in various other situations. You could only need to call this method directly if:

*   you know that client-side filtering is enabled ([ResultSet.useClientFiltering](#attr-resultsetuseclientfiltering):true) and active [ResultSet.allMatchingRowsCached](#method-resultsetallmatchingrowscached).
*   you have directly, programmatically modified data within the ResultSet such that it no longer matches the filter criteria
*   you want your modified records to disappear from the list of visible records (that is, those accessible via [ResultSet.get](#method-resultsetget))

**Flags**: A

---
## Method: ResultSet.find

### Description
Like [List.find](List.md#method-listfind). Checks only loaded rows and will not trigger a fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[Object](../reference.md#type-object)` — first matching object or null if not found

### Groups

- access
- find

---
## Method: ResultSet.transformData

### Description
`transformData()` provides an opportunity to modify data that has been returned from the server, before it has been integrated into the client-side cache.

If data is not immediately suited for client-side use when it is returned from the ultimate data store, this method allows it to be transformed on the client so that such transform operations do not impact server scalability.

It is legal for `transformData()` to modify not only the records, but also their number (by modifying startRow and endRow on the [DSResponse](DSResponse.md#class-dsresponse) object).

See also [DataSource.transformResponse](DataSource.md#method-datasourcetransformresponse) for an alternative entry point which applies to all DSResponses for a DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Any](#type-any) | false | — | data returned from the server |
| dsResponse | [DSResponse](#type-dsresponse) | false | — | the DSResponse object returned by the server |

### Returns

`[Array of Objects](#type-array-of-objects)` — the modified data, ready to be cached

---
## Method: ResultSet.allMatchingRowsCached

### Description
Do we have a complete client-side cache of records for the current filter criteria?

Returns `false` if this is a paged data set, and the entire set of records that match the current criteria has not been retrieved from the server. In other words, a return value of `false` means that this `ResultSet` has a partial cache.

### Returns

`[boolean](../reference.md#type-boolean)` — whether all matching rows are cached

**Flags**: A

---
## Method: ResultSet.setSort

### Description
Sort this ResultSet by the passed list of [SortSpecifier](../reference.md#object-sortspecifier)s.

If the ResultSet is already sorted and this method is called with an identical list of specifiers, this method will no-op. To cause data to be resorted with the same set of specifiers, use [resort()](#method-resultsetresort).

To clear an existing sort, pass in explicit null or empty array.

---
## Method: ResultSet.dataArrived

### Description
Notification fired when data has arrived from the server and has been successfully integrated into the cache.

When `dataArrived()` fires, an immediate call to `getRange()` with the `startRow` and `endRow` passed as arguments will return a List with no [loading markers](#classmethod-resultsetgetloadingmarker).

Note that `dataArrived()` won't fire in the case of the owning component filtering with unchanged criteria (for example using [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata) or [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata)). To support backward compatibility, the property [ResultSet.reapplyUnchangedLocalFilter](#attr-resultsetreapplyunchangedlocalfilter) can be set to force `dataArrived()` to be called if the ResultSet is [filtering locally](#method-resultsetfilterlocaldata) and the criteria haven't changed but are narrower than the criteria used to fetch the current cache.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | starting index of rows that have just loaded |
| endRow | [int](../reference.md#type-int) | false | — | ending index of rows that have just loaded, non-inclusive |

---
## Method: ResultSet.findByKey

### Description
Attempt to find the record in the resultSet that has a primary key value that matches the passed in parameter value. Only the locally cached data will be searched. Checks only loaded rows and will not trigger a fetch. Returns null if there is no match, data is not loaded, or there is no [dataSource](#attr-resultsetdatasource).

Note, if you pass a simple value to this method, it will be matched against the first primaryKey field. For DataSources with a composite primary key (multiple primaryKey fields), pass a criteria object containing just your primaryKeys, like this: `{ firstPkField: "value", secondPkField: 25 }`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| keyValue | [Object](../reference.md#type-object) | false | — | primary key value to search for |

### Returns

`[Record](#type-record)` — the record with a matching primary key field, or null if not found

---
## Method: ResultSet.getCachedRange

### Description
Returns the index of the first and last cached row around a given row, or null if the row itself is not cached. The last cached row value is inclusive.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row to check |

### Returns

`[Array of int](#type-array-of-int)` — first and last cached row indices, or null

**Flags**: A

---
## Method: ResultSet.applyFilter

### Description
The ResultSet will call applyFilter() when it needs to determine whether rows match the current filter criteria.

Default behavior is to call [DataSource.applyFilter](DataSource.md#method-datasourceapplyfilter) to determine which rows match that provided criteria.

Override this method or [DataSource.applyFilter](DataSource.md#method-datasourceapplyfilter) to implement your own client-side filtering behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Array](#type-array) | false | — | the list of rows |
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | the filter criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | dataSource request properties |

### Returns

`[Array](#type-array)` — the list of matching rows

**Flags**: A

---
## Method: ResultSet.lengthIsKnown

### Description
Whether the ResultSet knows the length of its data set.

When the ResultSet fetches data from the DataSource in response to [ResultSet.getRange](#method-resultsetgetrange) or similar methods, [DSResponse.totalRows](DSResponse.md#attr-dsresponsetotalrows) from the fetch lets the ResultSet know the full dataset size.

Prior to the completion of the first fetch, (or after [dropping cache](#method-resultsetinvalidatecache)) the ResultSet will not know how many records are available. At this time `lengthIsKnown()` will return false, and a call to [ResultSet.getLength](#method-resultsetgetlength) will return an arbitrary, large value.

Note: If [progressive loading](DataSource.md#attr-datasourceprogressiveloading) is active the reported [DSResponse.totalRows](DSResponse.md#attr-dsresponsetotalrows) value may not accurately reflect the true dataset size on the server. In this case `lengthIsKnown()` returns true, but the [reported length](#method-resultsetgetlength) of the ResultSet may change as additional rows are retrieved from the server. The [ResultSet.lengthIsProgressive](#method-resultsetlengthisprogressive) method will indicate when the resultSet is in this state.

### Returns

`[boolean](../reference.md#type-boolean)` — whether length is known

---
## Method: ResultSet.getCombinedCriteria

### Description
Returns a copy of all [explicit](#attr-resultsetcriteria) and [implicit](#method-resultsetgetimplicitcriteria) criteria currently applied to this `ResultSet`.

### Returns

`[Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria)` — combined criteria

---
## Method: ResultSet.getValueMap

### Description
Get a map of the form `{ item[idField] -> item[displayField] }`, for all items in the list. If more than one item has the same `idProperty`, the value for the later item in the list will clobber the value for the earlier item.

If this method is called when the [cache is incomplete](#method-resultsetallmatchingrowscached), it will trigger fetches, and will return a valueMap reflecting only the currently loaded rows.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| idField | [String](#type-string) | false | — | Property to use as ID (data value) in the valueMap |
| displayField | [String](#type-string) | false | — | Property to use as a display value in the valueMap |

### Returns

`[Object](../reference.md#type-object)` — valueMap object

### See Also

- [ResultSet.allMatchingRowsCached](#method-resultsetallmatchingrowscached)

---
## Method: ResultSet.willFetchData

### Description
Will changing the criteria for this resultSet require fetching new data from the server, or can the new criteria be satisfied from data already cached on the client?  
Second `textMatchStyle` parameter determines whether a change of text-match style will require a server fetch - for example if filter is being changed between an exact match (from e.g: [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata)) and a substring match (from e.g: [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata)).  
This method can be used to determine whether [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata) or [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata) would cause a server side fetch when passed a certain set of criteria.

Note that to predict correctly the decision that will be made by filter/fetch, you'll need to pass the same [TextMatchStyle](../reference.md#type-textmatchstyle) that will be used by the future filter/fetch. Fetching manually (e.g. [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata)) will by default use "exact" while filtering (e.g. [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata)) will by default use "substring". If the component is configured for autofetch (i.e. [ListGrid.autoFetchData](ListGrid_1.md#attr-listgridautofetchdata): true), that will use [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle), which defaults to "substring". If nothing/null is passed for the style, this method assumes you want the style from the last filter/fetch.

To determine what [TextMatchStyle](../reference.md#type-textmatchstyle) is being used, check the RPC Tab of the [SmartClient Developer Console](../kb_topics/debugging.md#kb-topic-debugging) and check the relevant [DSRequest](../reference.md#object-dsrequest).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new criteria to test. |
| textMatchStyle | [TextMatchStyle](../reference.md#type-textmatchstyle) | true | — | New text match style. If not passed, assumes textMatchStyle will not be modified. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if server fetch would be required to satisfy new criteria.

---
## Method: ResultSet.sortByProperty

### Description
Sort this ResultSet by a property of each record.

Sorting is performed on the client for a ResultSet that has a full cache for the current filter criteria. Otherwise, sorting is performed by the server, and changing the sort order will invalidate the cache.

**NOTE:** normalizers are not supported by ResultSets in "paged" mode, although valueMaps in the DataSource are respected by the SQLDataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to sort by |
| up | [boolean](../reference.md#type-boolean) | false | — | true == sort ascending, false == sort descending |
| normalizer | [Function](#type-function)|[ValueMap](../reference_2.md#type-valuemap) | true | — | May be specified as a function, with signature `normalize(item, propertyName, context)`, where `item` is a pointer to the item in the array, `propertyName` is the property by which the array is being sorted, and `context` is the arbitrary context passed into this method. Normalizer function should return the value normalized for sorting.  
May also be specified as a ValueMap which maps property values to sortable values. |
| context | [Any](#type-any) | true | — | Callers may pass an arbitrary context into the sort method, which will then be made available to the normalizer function |

### Returns

`[List](#type-list)` — the list itself

### Groups

- sorting

---
## Method: ResultSet.getLength

### Description
Return the total number of records that match the current filter criteria.

This length can only be known, even approximately, when the first results are retrieved from the server. Before then, the ResultSet returns a large length in order to encourage viewers to ask for rows. [ResultSet.lengthIsKnown()](#method-resultsetlengthisknown) can be called to determine whether an actual length is known.

Note that if [progressive loading](DataSource.md#attr-datasourceprogressiveloading) is active, the length advertised by the server may not be an accurate total row count for the data set. [ResultSet.lengthIsProgressive()](#method-resultsetlengthisprogressive) can be called to determine whether this is the case.

### Returns

`[Number](#type-number)` — number of items in the list

### Groups

- access

---
## Method: ResultSet.compareCriteria

### Description
Default behavior is to call [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria) to determine whether new criteria is guaranteed more restrictive, equivalent to the old criteria, or not guaranteed more restrictive, returning 1, 0 or -1 respectively. See [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria) for a full explanation of the default behavior.

Override this method or [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria) to implement your own client-side filtering behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new filter criteria |
| oldCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | old filter criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | dataSource request properties |
| policy | [String](#type-string) | true | — | overrides [CriteriaPolicy](../reference.md#type-criteriapolicy) |

### Returns

`[Number](#type-number)` — 0 if the filters are equivalent, 1 if newFilter is guaranteed more restrictive, and -1 if newFilter is not guaranteed more restrictive

### See Also

- [CriteriaPolicy](../reference.md#type-criteriapolicy)

---
## Method: ResultSet.findIndex

### Description
Like [List.findIndex](List.md#method-listfindindex). Checks only loaded rows and will not trigger a fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[int](../reference.md#type-int)` — index of the first matching Object or -1 if not found

### Groups

- access
- find

---
## Method: ResultSet.getSort

### Description
Return the current sort-specification for this ResultSet as an Array of [SortSpecifier](../reference.md#object-sortspecifier)s.

### Returns

`[Array of SortSpecifier](#type-array-of-sortspecifier)` — the list of [SortSpecifier](../reference.md#object-sortspecifier)s currently applied to this ResultSet

---
## Method: ResultSet.rowIsLoaded

### Description
Whether the given row has been loaded.

Unlike get(), will not trigger a server fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row to check |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the given row has been loaded, false if it has not been loaded or is still in the process of being loaded

**Flags**: A

---
## Method: ResultSet.indexOf

### Description
Return the position in the list of the first instance of the specified object.

If pos is specified, starts looking after that position.

Returns -1 if not found.

**NOTE:** ResultSet.indexOf() only inspects the current cache of records, so it is only appropriate for temporary presentation purposes. For example, it would not be appropriate to hold onto a record and attempt to use indexOf() to determine if it had been deleted.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to look for |
| pos | [number](#type-number) | true | — | earliest index to consider |
| endPos | [number](#type-number) | true | — | last index to consider |

### Returns

`[number](#type-number)` — position of the item, if found, -1 if not found

### Groups

- access

---
## Method: ResultSet.invalidateCache

### Description
Manually invalidate this ResultSet's cache.

Generally a ResultSet will observe and incorporate updates to the DataSource that provides its records, but when this is not possible, `invalidateCache()` allows manual cache invalidation.

`invalidateCache()` fires `dataChanged()`, which may cause components using this ResultSet to request new data for display, triggering server fetches.

**Flags**: A

---
## Method: ResultSet.getAllVisibleRows

### Description
Returns all rows that match the current criteria.

This method will not trigger a fetch to load more records. `getAllVisibleRows()` will return null if [ResultSet.lengthIsKnown](#method-resultsetlengthisknown) is false.

Records are returned in a new List but the Records within it are the same instances that the ResultSet is holding onto. Hence it's safe to add or remove records from the List without affecting the ResultSet but modifying the Records themselves is a direct modification of the client-side cache.

### Returns

`[Array of Record](#type-array-of-record)` — the records in the cache that match the current criteria, possibly null

**Flags**: A

---
## Method: ResultSet.allRowsCached

### Description
Do we have a complete client-side cache of all records for this DataSource?

Becomes true only when the ResultSet obtains a complete cache after a fetch with empty criteria.

### Returns

`[boolean](../reference.md#type-boolean)` — whether all rows are cached

**Flags**: A

---
## Method: ResultSet.duplicate

### Description
Returns a clone of this ResultSet sharing the same DataSource, current criteria, sort direction and cache state.

Internal caches are copied such that methods such as [ResultSet.lengthIsKnown](#method-resultsetlengthisknown), [ResultSet.allMatchingRowsCached](#method-resultsetallmatchingrowscached) and [ResultSet.allRowsCached](#method-resultsetallrowscached) return identical results for the new ResultSet.

Subsequent changes to criteria or sort direction on the original ResultSet with not affect the duplicate, and vice versa. Outstanding fetches on the original ResultSet will likewise have no effect on the duplicate when they complete. However, actual Record instances are shared between the original and copied ResultSet, so direct modification of Records will affect both ResultSets.

The new ResultSet will listen for DataSource changes and automatically update caches just as normal ResultSets do.

**NOTE:** if you are looking for a simple list of Records rather than a new, fully functional ResultSet, consider [ResultSet.getAllCachedRows](#method-resultsetgetallcachedrows) or [ResultSet.getAllVisibleRows](#method-resultsetgetallvisiblerows). If you are looking to create a filterable, sortable subset of the current ResultSet, consider creating a new ResultSet and passing the results of `getAllCachedRows` or `getAllVisibleRows` as the initial value of ResultSet.allRows.

### Returns

`[ResultSet](#type-resultset)` — new ResultSet sharing the same DataSource, current criteria, sort direction and cache state.

---
## Method: ResultSet.setFullLength

### Description
Set the total number of rows available from the server that match the current filter criteria for this ResultSet.

This is an advanced feature. One use case for this method would be for a ResultSet populated with [progressive loading](../kb_topics/progressiveLoading.md#kb-topic-progressive-loading) - if application code determines an accurate row count for the current filter criteria it may be applied directly to the ResultSet via this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| length | [number](#type-number) | false | — | total rows available from the server |

**Flags**: A

---
## Method: ResultSet.usingFilteredData

### Description
Determine whether the ResultSet is showing a filtered, proper subset of the cached rows. This happens if [client filtering](#attr-resultsetuseclientfiltering) is enabled. Rows may have been loaded from the server when a more restrictive criteria is applied such that filtering could be performed on the client side.

This method returns false if data is not loaded yet.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the ResultSet is showing a filtered subset of the cached rows, false otherwise.

### See Also

- [ResultSet.getAllCachedRows](#method-resultsetgetallcachedrows)

---
## Method: ResultSet.setCriteria

### Description
Set the filter criteria to use when fetching rows.

Depending on the result of [ResultSet.compareCriteria](#method-resultsetcomparecriteria) and settings for [ResultSet.useClientFiltering](#attr-resultsetuseclientfiltering) / [FetchMode](../reference_2.md#type-fetchmode), setting criteria may cause a trip to the server to get a new set of rows, or may simply cause already-fetched rows to be re-filtered according to the new Criteria. In either case, the dataset length available from [ResultSet.getLength](#method-resultsetgetlength) may change and rows will appear at different indices.

The filter criteria can be changed while server fetches for data matching the old criteria are still outstanding. If this is the case, the ResultSet will make sure that any records received matching the old criteria are not added to the cache for the new criteria. Any callbacks for responses to the outstanding requests are fired as normal, and the responses' [totalRows](DSResponse.md#attr-dsresponsetotalrows) counts are kept (as they are still potentially meaningful to components using the ResultSet), but the response data is cleared so that it won't be used inadvertently as data matching the new criteria.

Note: for simple Criteria, any field values in the criteria explicitly specified as null will be passed to the server. By default the server then returns only records whose value is null for that field. This differs from certain higher level methods such as [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata) which prune null criteria fields before performing a fetch operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | the filter criteria |

### Returns

`[boolean](../reference.md#type-boolean)` — Returns false if the new criteria match the previous criteria, implying the data is unchanged.

---
## Method: ResultSet.get

### Description
Returns the record at the specified position.

All List access methods of the ResultSet have the semantics described in `getRange()`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [Number](#type-number) | false | — | position of the element to get |

### Returns

`[Object](../reference.md#type-object)` — whatever's at that position, or `undefined` if not found

### Groups

- access

### See Also

- [ResultSet.getRange](#method-resultsetgetrange)

---
## Method: ResultSet.setAllRows

### Description
Update the [ResultSet.allRows](#attr-resultsetallrows) client-side cache of data at runtime.

This method is useful for cases where a full, unfiltered set of data is present on the client and developers wish to filter that data-set locally without going through a fetch operation against a DataSource.

Developers using this pattern may also wish to consider the [FilteredList](FilteredList.md#class-filteredlist) class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| allRows | [Array of Records](#type-array-of-records) | false | — | New set of unfiltered cache data |

**Flags**: A

---
## Method: ResultSet.findAll

### Description
Like [List.findAll](List.md#method-listfindall). Checks only loaded rows and will not trigger a fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[Array](#type-array)` — all matching Objects or null if none found

### Groups

- access
- find

---
## Method: ResultSet.unsort

### Description
Clear any [sort specifiers](#method-resultsetsetsort) applied to this ResultSet, while maintaining the current order of records. This feature is not supported for all lists. This method returns true if supported.

If a [paged resultSet](#resultsetdatafetchmode) has a partial cache, the order of records in the local data must always match the order of records as provided by the [DataSource](DataSource.md#class-datasource) - otherwise the wrong set of records will be returned as new pages of data are fetched (in response to a user scrolling a ListGrid, for example).

It's therefore not possible to unsort a paged resultSet with a partial cache and maintain the current order of any loaded records. If this method is called on a resultSet in this state, it will always no-op and return false.

If you need to force a partially loaded ResultSet to discard it's current sort, and explicit call to [setSort(null)](#method-resultsetsetsort) may be used. This will drop the current sort specifiers and [ResultSet.invalidateCache](#method-resultsetinvalidatecache).

### Returns

`[boolean](../reference.md#type-boolean)` — true == list supports unsorting, false == not supported.

### Groups

- sorting

**Flags**: A

---
## Method: ResultSet.getAllCachedRows

### Description
Returns a list of all rows that have been cached. This is potentially a superset of all rows that are available via [ResultSet.getAllVisibleRows](#method-resultsetgetallvisiblerows) if the ResultSet is using client-side filtering to display a subset of loaded rows (see the [ResultSet overview](#class-resultset)).

If [ResultSet.usingFilteredData](#method-resultsetusingfiltereddata) returns false, this is the same list as would be returned by [ResultSet.getAllVisibleRows](#method-resultsetgetallvisiblerows).

This method will not trigger a fetch to load more records. getAllCachedRows() will return null if [ResultSet.lengthIsKnown](#method-resultsetlengthisknown) is false.

Records are returned in a new List but the Records within it are the same instances that the ResultSet is holding onto. Hence it's safe to add or remove records from the List without affecting the ResultSet but modifying the Records themselves is a direct modification of the client-side cache.

### Returns

`[Array of Record](#type-array-of-record)` — the records in the cache, possibly null

**Flags**: A

---
## Method: ResultSet.getCriteria

### Description
Get the current criteria for this ResultSet.

### Returns

`[Criteria](../reference_2.md#type-criteria)` — current criteria

---
## Method: ResultSet.lengthIsProgressive

### Description
Does the length of this ResultSet as returned by [ResultSet.getLength](#method-resultsetgetlength) reflect the [totalRows](DSResponse.md#attr-dsresponsetotalrows) reported by a DataSource with [progressiveLoading](../kb_topics/progressiveLoading.md#kb-topic-progressive-loading) enabled?

If true, this row count may not be an accurate reflection of the true size of the data set.

This method relies on the [DSResponse.progressiveLoading](DSResponse.md#attr-dsresponseprogressiveloading) attribute having been set accurately by the server. Note that if the user has scrolled to the end of a progressively loaded data set, or [ResultSet.setFullLength](#method-resultsetsetfulllength) has been explicitly called, this method will no longer return true.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the length of this ResultSet was derived from a [progressiveLoading:true](DSResponse.md#attr-dsresponseprogressiveloading) dsResponse.

### Groups

- progressiveLoading

---
## Method: ResultSet.findNextIndex

### Description
Like [List.findNextIndex](List.md#method-listfindnextindex). Checks only loaded rows and will not trigger a fetch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startIndex | [int](../reference.md#type-int) | false | — | first index to consider. |
| propertyName | [String](#type-string)|[Function](#type-function)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match; or, if a function is passed, the predicate function to call; or, if an object is passed, set of properties and values to match. |
| value | [Any](#type-any) | true | — | value to compare against (if `propertyName` is a string) or the value of `this` when the predicate function is invoked (if `propertyName` is a function) |
| endIndex | [int](../reference.md#type-int) | true | — | last index to consider (inclusive). |

### Returns

`[int](../reference.md#type-int)` — index of the first matching value or -1 if not found.

### Groups

- access
- find

---
## Method: ResultSet.getRange

### Description
Return the items between position start and end, non-inclusive at the end, possibly containing markers for records that haven't loaded yet.

Calling getRange for records that have not yet loaded will trigger an asynchronous fetch. The returned data will contain the [loading marker](#classmethod-resultsetgetloadingmarker) as a placeholder for records being fetched. If any rows needed to be fetched, `dataArrived()` will fire when they arrive.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start position |
| end | [number](#type-number) | false | — | end position |

### Returns

`[Array](#type-array)` — subset of the array from start -> end-1

### Groups

- access

### See Also

- [ResultSet.getLoadingMarker](#classmethod-resultsetgetloadingmarker)
- [ResultSet.dataArrived](#method-resultsetdataarrived)

---
