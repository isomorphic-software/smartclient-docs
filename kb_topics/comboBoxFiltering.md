# ComboBoxItem PickList Filtering

[← Back to API Index](../reference.md)

---

## KB Topic: ComboBoxItem PickList Filtering

### Description
The criteria used to decide which options should appear in the drop-down [PickList](../reference_2.md#interface-picklist) shown by a ComboBox are determined as follows.

While the user is typing in a value, the [ComboBoxItem.getPickListFilterCriteria](../classes/ComboBoxItem.md#method-comboboxitemgetpicklistfiltercriteria) method will return the typed-in value as part of the criteria, so that only matching values are shown. Matching is determined by the [textMatchStyle](../classes/ComboBoxItem.md#attr-comboboxitemtextmatchstyle). Note that the [ComboBoxItem.filterFields](../classes/ComboBoxItem.md#attr-comboboxitemfilterfields) attribute may be used to determine which fields filtering is performed against for databound comboBoxItems.

If the user explicitly shows the down-down pickList, via either clicking on the drop down icon or using the _Ctrl+Arrow Down_ key combination, the typed-in value is ignored for filtering.

If included in the criteria, the typed-in value will be included as a value for the [displayField](../classes/ComboBoxItem.md#attr-comboboxitemdisplayfield) (or for the [valueField](../classes/ComboBoxItem.md#attr-comboboxitemvaluefield) if `this.displayField` is unspecified).

Static criteria, specified via [optionCriteria](../classes/FormItem.md#attr-formitemoptioncriteria) or [pickListCriteria](../classes/ComboBoxItem.md#attr-comboboxitempicklistcriteria), will always be included by the default implementation (combined with the typed in value if appropriate).

`getPickListFilterCriteria()` may be overridden for custom behavior. If you are implementing your own pickList filter criteria, the **read-only** property [this.filterWithValue](../classes/ComboBoxItem.md#attr-comboboxitemfilterwithvalue) can be read to determine whether the ComboBox would ordinarily ignore the typed-in value for filtering. Note that in addition to cases where the user explicitly shows the pickList, `filterWithValue` will also be `true` during a call to [ComboBoxItem.fetchData](../classes/ComboBoxItem.md#method-comboboxitemfetchdata) on a databound comboBox.

**NOTE:** The defaut implementation of this method will return an [AdvancedCriteria](../reference.md#object-advancedcriteria) object if multiple [ComboBoxItem.filterFields](../classes/ComboBoxItem.md#attr-comboboxitemfilterfields) are specified, or if there are field collisions between any specified static [optionCriteria](../classes/FormItem.md#attr-formitemoptioncriteria), [pickListCriteria](../classes/ComboBoxItem.md#attr-comboboxitempicklistcriteria) and the entered value. AdvancedCriteria are not supported by all DataSource types, including the built-in server-side SQL dataSources in SmartClient Pro edition (though they are supported by SQL dataSources in Power and Enterprise editions).

**Client-Side Filtering**  
By default, the ComboBoxItem will automatically use client-side filtering whenever it receives a complete set of results for a given search string, and then the user types more letters (so reducing the results further).

Client-side filtering may malfunction if the server filtering behavior can't be replicated client-side (for example, Google Search). To disable client-side filtering so that the comboBox always contacts the server for data whenever the use changes the search string, set [ComboBoxItem.useClientFiltering](../classes/ComboBoxItem.md#attr-comboboxitemuseclientfiltering) to false.

However, disabling client-side filtering will slow down the UI and cause more round-trips to the server, so if client-side filtering is malfunctioning but _should work_, try to correct the problem rather than disable the feature.

For example, if the initial search works correctly but adding more letters always causes zero matches, most likely the Records returned by the server lack values for the field(s) targeted by the filter criteria, or the field values returned by the server don't match the criteria values.

View the returned data in the RPC tab in the Developer Console and enable the "ResultSet" log category in the "Results" tab to troubleshoot how the filter criteria are being applied to data, and look closely at your settings for [valueField](../classes/ComboBoxItem.md#attr-comboboxitemvaluefield) and [displayField](../classes/ComboBoxItem.md#attr-comboboxitemdisplayfield).

---
