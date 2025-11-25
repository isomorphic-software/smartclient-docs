# Progressive Loading

[← Back to API Index](../main.md)

---

## KB Topic: Progressive Loading

### Description
The "Progressive Loading" pattern is a way to deal with incrementally retrieving large data sets on demand (see the **Paging and total dataset length** section of the [ResultSet documentation](../classes/ResultSet.md#class-resultset)), when the total data length is not available. For example - if a row-count database query to retrieve an accurate data count would be prohibitively slow, you may opt to make use of progressive loading instead.

In progressive loading mode, the reported [DSResponse.totalRows](../classes/DSResponse.md#attr-dsresponsetotalrows) from a fetch will not be guaranteed to be accurate as long as there are more rows to be fetched beyond the [requested endRow](../classes/DSRequest.md#attr-dsrequestendrow). Instead the `response.totalRows` will be set to the requested endRow plus the configured [DataSource.endGap](../classes/DataSource.md#attr-datasourceendgap). This indicates to the application that more rows are available, and as the user scrolls to access these rows, additional fetch operations will occur to retrieve the extra rows, and will report a new `totalRows` value.

Note that when progressive loading is active, the user will typically not be able to cause direct movement to some arbitrary position in the dataset (as is the case with ordinary, non-progressive loading).

When the user scrolls to the true end of the data-set, the `totalRows` value is expected to be accurate.

### Related

- [ResultSet.lengthIsProgressive](../classes/ResultSet.md#method-resultsetlengthisprogressive)
- [DataBoundComponent.progressiveLoading](../classes/DataBoundComponent.md#attr-databoundcomponentprogressiveloading)
- [DataSource.progressiveLoading](../classes/DataSource.md#attr-datasourceprogressiveloading)
- [DataSource.progressiveLoadingThreshold](../classes/DataSource.md#attr-datasourceprogressiveloadingthreshold)
- [DataSource.lookAhead](../classes/DataSource.md#attr-datasourcelookahead)
- [DataSource.endGap](../classes/DataSource.md#attr-datasourceendgap)
- [DSRequest.progressiveLoading](../classes/DSRequest.md#attr-dsrequestprogressiveloading)
- [OperationBinding.progressiveLoading](../classes/OperationBinding.md#attr-operationbindingprogressiveloading)
- [ResultSet.progressiveLoading](../classes/ResultSet.md#attr-resultsetprogressiveloading)
- [ResultSet.rememberDynamicProgressiveLoading](../classes/ResultSet.md#attr-resultsetrememberdynamicprogressiveloading)
- [ResultTree.progressiveLoading](../classes/ResultTree.md#attr-resulttreeprogressiveloading)
- [SelectItem.progressiveLoading](../classes/SelectItem.md#attr-selectitemprogressiveloading)
- [ComboBoxItem.progressiveLoading](../classes/ComboBoxItem.md#attr-comboboxitemprogressiveloading)

---
