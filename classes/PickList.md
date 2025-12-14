# PickList Documentation

[← Back to API Index](../reference.md)

---

## ClassAttr: PickList.selectAllStoredValue

### Description
Special constant used to indicate that choosing this value from the [PickList.specialValues](#attr-picklistspecialvalues) list should result in selecting all of the values of the field. Only for use with `specialValues` - cannot be used elsewhere.  
This attribute may only be used when all matching records are being loaded, not when data paging is in use.

**Flags**: IR

---
## ClassAttr: PickList.emptyStoredValue

### Description
Special constant used to indicate that choosing this value from the [PickList.specialValues](#attr-picklistspecialvalues) list should result in clearing the value of the field. Only for use with `specialValues` - cannot be used elsewhere.

**Flags**: IR

---
## Attr: PickList.clickMaskMode

### Description
Determines the behavior of the click-mask thrown up when this pickList is visible.

The default value, "hard", matches the familiar behavior of combos and selects on Windows, Mac and other platforms - mouse-events such as rollovers are blocked and, when a click is received, the picker is hidden and the event is cancelled.

When `clickMaskMode` is "soft", mouse-events continue to fire, meaning that rollover styles, for example, continue to be updated. When a click is received in this mode, the picker is hidden and the click event is allowed to proceed to its target - this means that clicking an item with an open picker will re-open the picker.

**Flags**: IRW

---
## Attr: PickList.showAllOptions

### Description
If true, even non-matching options will be shown, with configurable [separator rows](#attr-picklistseparatorrows) in between. Not valid for [databound pickLists](#attr-picklistoptiondatasource).

**Flags**: IR

---
## Attr: PickList.pickListWidth

### Description
Default width to show the pickList. If not specified, the width of this form item's element will be used instead.

Note that this is a minimum value - by default if the values displayed in this pickList are wider than the specified width the list will expand to accommodate them.

### Groups

- pickList

**Flags**: IRW

---
## Attr: PickList.singleClickFolderToggle

### Description
When this item is showing a [tree-based picker](#attr-picklistdatasettype), the default behavior is for folder open-state to be toggled by double-clicking. Set this attribute to true to toggle folders on a single-click instead.

Note: when set to true, users can only choose leaf-nodes, since clicking folders would simply toggle them.

**Flags**: IR

---
## Attr: PickList.rootNodeId

### Description
When this item is showing a [tree-based picker](#attr-picklistdatasettype), this is the [id](SelectItem.md#attr-selectitemvaluefield) of the record to use as the [root](Tree.md#attr-treerootvalue) node.

**Flags**: IRW

---
## Attr: PickList.useClientFiltering

### Description
For [databound](#attr-picklistoptiondatasource) items, this property will be passed to the generated ResultSet data object for the pickList as [ResultSet.useClientFiltering](ResultSet.md#attr-resultsetuseclientfiltering). Setting to false will disable filtering on the client and ensure criteria are always passed to the DataSource directly.

**Flags**: IRA

---
## Attr: PickList.filterLocally

### Description
If `filterLocally` is set for this item, and this item is showing options from a dataSource, fetch the entire set of options from the server, and use these values to map the item value to the appropriate display value. Also use `"local"` type filtering on drop down list of options.

This means data will only be fetched once from the server, and then filtered on the client.

Note - when this property is set to `false`, filtering will still be performed on the client if a complete set of data for some criteria has been cached by a fetch, and a subsequent fetch has more restrictive criteria. To explicitly disable client-side filtering set the [PickList.useClientFiltering](#attr-picklistuseclientfiltering) property to false.

### See Also

- [FormItem.filterLocally](FormItem.md#attr-formitemfilterlocally)

**Flags**: IRA

---
## Attr: PickList.pickListAnimationTime

### Description
If [PickList.animatePickList](#attr-picklistanimatepicklist) is true, this attribute specifies the millisecond duration of the animation effect.

### Groups

- pickList

**Flags**: IRWA

---
## Attr: PickList.pickListConstructor

### Description
The Class to use when creating a picker of [type "list"](#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickListMenu](PickListMenu.md#class-picklistmenu).

### Groups

- pickList

**Flags**: IR

---
## Attr: PickList.optionFilterContext

### Description
If this item has a specified `optionDataSource`, and this property is not null, this will be passed to the datasource as [DSRequest](../reference.md#object-dsrequest) properties when performing the filter operation on the dataSource to obtain the set of options for the list. This provides, among other capabilities, a way to trigger the server to return summary records.

### See Also

- [serverSummaries](../kb_topics/serverSummaries.md#kb-topic-server-summaries)

**Flags**: IRA

---
## Attr: PickList.emptyPickListHeight

### Description
Height for an empty pick list (showing the empty message), if the pick list has no records and [PickList.hideEmptyPickList](#attr-picklisthideemptypicklist) is `false`.

**Flags**: IRW

---
## Attr: PickList.valueField

### Description
If this form item maps data values to display values by retrieving the [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) values from an [optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property denotes the the field to use as the underlying data value in records from the optionDataSource.  
If not explicitly supplied, the valueField name will be derived as described in [FormItem.getValueFieldName](FormItem.md#method-formitemgetvaluefieldname).

### Groups

- databinding

**Flags**: IRA

---
## Attr: PickList.pickListTallBaseStyle

### Description
Optional [tallBaseStyle](ListGrid_1.md#attr-listgridtallbasestyle) for pickList cells. If unset, [PickList.pickListBaseStyle](#attr-picklistpicklistbasestyle) will be applied to all cells.

### Groups

- pickList

**Flags**: IR

---
## Attr: PickList.pickListHeight

### Description
Maximum height to show the pick list before it starts to scroll. Note that by default the pickList will be sized to the height required by its content so it will be taller when more rows are available as selectable options

### Groups

- pickList

**Flags**: IRW

---
## Attr: PickList.sortField

### Description
Specifies one or more fields by which this item should be initially sorted. It can be a [field name](ListGridField.md#attr-listgridfieldname), or an array of field names - but note that, if multiple fields are supplied, then each will be sorted in the same [direction](ListGrid_1.md#attr-listgridsortdirection).

For full sorting control, set [initialSort](#attr-picklistinitialsort) to a list of custom [sortSpecifiers](../reference.md#object-sortspecifier).

This attribute can also be set to the index of a field in the fields array, but note that it will be converted to a string (field name) after initialization.

### Groups

- sorting

**Flags**: IR

---
## Attr: PickList.dataSetType

### Description
Whether to show the picker as a flat list, or a collapsible tree.

The default value, "list", will use an instance of the [pickListConstructor](#attr-picklistpicklistconstructor) as the picker - "tree" will show an instance of [pickTreeConstructor](#attr-picklistpicktreeconstructor).

**Flags**: IR

---
## Attr: PickList.valueIconField

### Description
For Databound formItems, this property determines which column [FormItem.valueIcons](FormItem.md#attr-formitemvalueicons) should show up in for this formItem's pickList.  
If unset, valueIcons show up in the [PickList.displayField](#attr-picklistdisplayfield) column if specified, otherwise the [PickList.valueField](#attr-picklistvaluefield) column.  
In most cases only the `displayField` or `valueField` will be visible. This property is typically only required if custom [PickList.pickListFields](#attr-picklistpicklistfields) have been specified for this item.

### See Also

- [FormItem.valueIcons](FormItem.md#attr-formitemvalueicons)
- [PickList.pickListFields](#attr-picklistpicklistfields)

**Flags**: IRWA

---
## Attr: PickList.emptyPickListMessage

### Description
Message to display in the pickList if there's no data and [PickList.hideEmptyPickList](#attr-picklisthideemptypicklist) is `false`.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: PickList.initialSort

### Description
An array of [SortSpecifier](../reference.md#object-sortspecifier) objects used to set up the initial sort configuration for this pickList. If specified, this will be used instead of any [PickList.sortField](#attr-picklistsortfield) specified.

### Groups

- sorting

**Flags**: IR

---
## Attr: PickList.hideEmptyPickList

### Description
If this pickList contains no options, should it be hidden? If unset, default behavior is to allow the empty pickList to show if it is databound.

**Flags**: IRW

---
## Attr: PickList.pickList

### Description
ListGrid-based AutoChild created by the system to display a list of pickable options for this item.

The pickList is automatically generated and displayed by the system when necessary. It may be customized via properties such as [PickList.pickListConstructor](#attr-picklistpicklistconstructor), [PickList.pickTreeConstructor](#attr-picklistpicktreeconstructor), [PickList.pickListProperties](#attr-picklistpicklistproperties) and more. See the [PickList overview](../reference_2.md#interface-picklist) for more information.

Accessing the generated pickList at runtime is an advanced usage. In most cases developers should not modify this generated component directly but should instead use attributes on the formItem to configure it.

**Flags**: RA

---
## Attr: PickList.separatorRows

### Description
Array of records to show between matching and non-matching rows in the PickList.

Not valid for [databound pickLists](#attr-picklistoptiondatasource).

**Flags**: IR

---
## Attr: PickList.iconPlacement

### Description
For PickList items with [PickListItemIconPlacement](../reference.md#type-picklistitemiconplacement) set such that the pickList does not render near-origin, should specified [icons](FormItem.md#attr-formitemicons) be rendered inline within the formItem itself, or within the [pickerNavigationBar](ComboBoxItem.md#attr-comboboxitempickernavigationbar).

May be overridden at the icon level via [FormItemIcon.iconPlacement](FormItemIcon.md#attr-formitemiconiconplacement).

For mobile browsing with limited available screen space, icons rendered in the navigation bar may be easier for the user to interact with.

**Flags**: IR

---
## Attr: PickList.fetchDisplayedFieldsOnly

### Description
If this item has a specified `optionDataSource` and this property is `true`, the list of fields used by this pickList will be passed to the datasource as [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs). If the datasource supports this feature the returned fields will be limited to this list. A custom datasource will need to add code to implement field limiting.

This list of used fields consists of the values of [valueField](FormItem.md#attr-formitemvaluefield), [displayField](FormItem.md#attr-formitemdisplayfield) and [pickListFields](#attr-picklistpicklistfields).

NOTE: When enabled, [getSelectedRecord](FormItem.md#method-formitemgetselectedrecord) will only include the fetched fields.

**Flags**: IRA

---
## Attr: PickList.autoOpenTree

### Description
When this item is showing a [tree-based picker](#attr-picklistdatasettype), which nodes should be opened automatically. Options are:

*   "none" - no nodes are opened automatically
*   "root" - opens the [top-level node](#attr-picklistrootnodeid) - in databound tree-pickers, this node is always hidden
*   "all" - when [loading data on demand](ResultTree.md#attr-resulttreeloaddataondemand), opens the [top-level node](#attr-picklistrootnodeid) and all of it's direct descendants - otherwise, opens all loaded nodes

**Flags**: IRW

---
## Attr: PickList.pickTreeConstructor

### Description
The Class to use when creating a picker of [type "tree"](#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickTreeMenu](../reference.md#class-picktreemenu).

**Flags**: IR

---
## Attr: PickList.pickListBaseStyle

### Description
Base Style for pickList cells. See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the pickListBaseStyle to generate stateful cell styles.

Note: if [PickList.pickListTallBaseStyle](#attr-picklistpicklisttallbasestyle) is specified, this property will be used as the [normalBaseStyle](ListGrid_1.md#attr-listgridnormalbasestyle) and that property will be applied to cells that do not match the default cell height, or if [ListGrid.fastCellUpdates](ListGrid_1.md#attr-listgridfastcellupdates) is true for the pickList in Internet Explorer.

### Groups

- pickList

**Flags**: IR

---
## Attr: PickList.pickListHeaderHeight

### Description
If this pick list is showing multiple fields, this property determines the height of the column headers for those fields. Set to zero to suppress the headers entirely.

### Groups

- pickList

### See Also

- [PickList.pickListFields](#attr-picklistpicklistfields)

**Flags**: IRW

---
## Attr: PickList.useLocalDisplayFieldValue

### Description
If [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) is specified for a field, should the display value for the field be picked up from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues)?

This behavior is typically valuable for dataBound components where the displayField is specified at the DataSourceField level. See [DataSourceField.displayField](DataSourceField.md#attr-datasourcefielddisplayfield) for more on this.

Note that for DataSources backed by the [SmartClient server](../kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration), fields with a specified [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) and [DataSourceField.displayField](DataSourceField.md#attr-datasourcefielddisplayfield) will automatically have this property set to true if not explicitly set to false in the dataSource configuration.

Otherwise, if not explicitly set, local display value will be used unless:

*   This item has an explicitly specified optionDataSource, rather than deriving its optionDataSource from a specified [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) specification
*   The [FormItem.name](FormItem.md#attr-formitemname) differs from the [valueField](FormItem.md#method-formitemgetvaluefieldname) for the item

**Flags**: IRW

---
## Attr: PickList.useOptionTextMatchStyleInPickList

### Description
For databound pickList-based formItems, if there are both explicitly specified [FormItem.optionCriteria](FormItem.md#attr-formitemoptioncriteria) and [PickList.pickListCriteria](#attr-picklistpicklistcriteria), these will be combined when determining the final criteria for retrieving the set of data to display in the drop down pickList.

If the `optionCriteria` are specified as simple crition objects (rather than [AdvancedCriteria](../reference.md#object-advancedcriteria)) this property determines the textMatchStyle to apply to the optionCriteria - whether to use [FormItem.optionTextMatchStyle](FormItem.md#attr-formitemoptiontextmatchstyle) or consult [PickList.textMatchStyle](#attr-picklisttextmatchstyle).

Wherever possible, this property should be set to `true`, to ensure the optionCriteria are interpreted the same way when [fetching pickList data](#method-picklistgetpicklistfiltercriteria) as [when looking up a displayValue directly from the optionDataSource](FormItem.md#attr-formitemoptiondatasource).

However if the specified textMatchStyles do not match this will cause [AdvancedCriteria](../reference.md#object-advancedcriteria) to be generated by [PickList.getPickListFilterCriteria](#method-picklistgetpicklistfiltercriteria) even if both [optionCriteria](FormItem.md#attr-formitemoptioncriteria) and [pickListCriteria](#attr-picklistpicklistcriteria) are specified as simple criteria. Since not all DataSources support AdvancedCriteria developers may choose to set this value to false and avoid them being created.

**Flags**: IRA

---
## Attr: PickList.fetchDelay

### Description
For a ComboBox or other pickList that accepts user-entered criteria, how many milliseconds to wait after the last user keystroke before fetching data from the server. The default setting will initiate a fetch if the user stops typing or pauses briefly.

**Flags**: IRWA

---
## Attr: PickList.pickListApplyRowNumberStyle

### Description
Default value for [ListGrid.applyRowNumberStyle](ListGrid_1.md#attr-listgridapplyrownumberstyle) for this item's generated pickList.

### Groups

- pickList

**Flags**: IRWA

---
## Attr: PickList.pickListProperties

### Description
If specified this properties block will be applied to the [pickList](PickListMenu.md#class-picklistmenu) created for this FormItem.

_Note_: Not every ListGrid property is supported when assigned to a pickList. Where there is a dedicated API on the form item (such as [pickListCellHeight](#attr-picklistpicklistcellheight)), we recommend that be used in favor of setting the equivalent property on the `pickListProperties` block.

_PickLists and [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor):_  
[ComboBoxItems](ComboBoxItem.md#class-comboboxitem) do not support setting `showFilterEditor` to true on pickListProperties. This combination of settings leads to an ambiguous user experience as the two sets of filter-criteria (those from the text-box and those from the pickList filter editor) interact with each other.  
Setting [showFilterEditor:true](ListGrid_1.md#attr-listgridshowfiltereditor) in [SelectItem.pickListProperties](SelectItem.md#attr-selectitempicklistproperties) is a valid way to create a filterable pickList, on a SelectItem, but this setting is not supported on a SelectItem with [SelectItem.multiple](SelectItem.md#attr-selectitemmultiple) set to true - this combination of settings can cause a selected value to be filtered out of view at which point further selection changes will discard that value.  
In general we recommend the ComboBoxItem class (with [ComboBoxItem.addUnknownValues](ComboBoxItem.md#attr-comboboxitemaddunknownvalues) set as appropriate) as a better interface for filtering pickList data.

### Groups

- pickList

**Flags**: IR

---
## Attr: PickList.pickListFields

### Description
This property allows the developer to specify which field\[s\] will be displayed in the drop down list of options.

Only applies to databound pickLists (see [PickList.optionDataSource](#attr-picklistoptiondatasource), or pickLists with custom data set up via the advanced [PickList.getClientPickListData](#method-picklistgetclientpicklistdata) method.

If this property is unset, we display the [PickList.displayField](#attr-picklistdisplayfield), if specified, otherwise the [PickList.valueField](#attr-picklistvaluefield).

If there are multiple fields, column headers will be shown for each field, the height of which can be customized via the [PickList.pickListHeaderHeight](#attr-picklistpicklistheaderheight) attribute.

Each field to display should be specified as a [ListGridField](../reference_2.md#object-listgridfield) object. Note that unlike in [listGrids](ListGrid_1.md#class-listgrid), dataSource fields marked as [hidden:true](DataSourceField.md#attr-datasourcefieldhidden) will be hidden by default in pickLists. To override this behavior, ensure that you specify an explicit value for [showIf](ListGridField.md#method-listgridfieldshowif).

### Groups

- pickList

### See Also

- [PickList.valueField](#attr-picklistvaluefield)
- [PickList.pickListHeaderHeight](#attr-picklistpicklistheaderheight)

**Flags**: IRA

---
## Attr: PickList.pickListCriteria

### Description
If this item has a databound pickList (for example [PickList.optionDataSource](#attr-picklistoptiondatasource) is set), this property can be used to provide static filter criteria when retrieving the data for the pickList.

### Groups

- pickList

**Flags**: IRWA

---
## Attr: PickList.cachePickListResults

### Description
For databound pickLists (see [PickList.optionDataSource](#attr-picklistoptiondatasource)), by default SmartClient will cache and re-use datasets shown by pickLists in an LRU (least recently used) caching pattern.

Setting this flag to false avoids this caching for situations where it is too aggressive.

**Flags**: IR

---
## Attr: PickList.pickListCellHeight

### Description
Cell Height for this item's pickList.

### Groups

- pickList

**Flags**: IRW

---
## Attr: PickList.textMatchStyle

### Description
When applying filter criteria to pickList data, what type of matching to use.

For a databound pickList ([PickList.optionDataSource](#attr-picklistoptiondatasource) set), `textMatchStyle` is sent to the server as [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle).

For a non-databound pickList, `textMatchStyle` is applied by [filterClientPickListData()](#method-picklistfilterclientpicklistdata).

**Flags**: IR

---
## Attr: PickList.specialValues

### Description
A set of "special" values such as "All", "None" or "Invalid" that do not appear in the normal [ValueMap](../reference_2.md#type-valuemap) or in the data returned by the [PickList.optionDataSource](#attr-picklistoptiondatasource).

Like other uses of [ValueMap](../reference_2.md#type-valuemap), either a list of values or a mapping from stored to display value can be provided.

These values can either be shown at the top of the list of values (in the order specified), or can be shown in a separate, non-scrolling region - the setting [separateSpecialValues](SelectItem.md#attr-selectitemseparatespecialvalues) controls this. Note that data paging can only be used if `separateSpecialValues` is enabled.

If `specialValues` are configured, [allowEmptyValue](SelectItem.md#attr-selectitemallowemptyvalue) is ignored - an empty value, if desired, must be included in the `specialValues`. To provide a `specialValue` which clears the value of the field, use the special constant [PickList.emptyStoredValue](#classattr-picklistemptystoredvalue).

`specialValues` can also be used to take a value that _does_ appear in the normal data and redundantly display it at the top of the list to make it more accessible. Note that in this case it is expected that the special value appears _both_ at the top of the list _and_ in it's normal position in the list, so this works best with [separateSpecialValues](SelectItem.md#attr-selectitemseparatespecialvalues) mode enabled.

Also, if an [PickList.optionDataSource](#attr-picklistoptiondatasource) is used, [PickList.specialValues](#attr-picklistspecialvalues) that appear in the normal dataset _will_ be updated by automatic [cache synchronization](../reference.md#kb-topic-cachesync) (if the [PickList.displayField](#attr-picklistdisplayfield) is updated). However when using a distinct [PickList.valueField](#attr-picklistvaluefield) and [PickList.displayField](#attr-picklistdisplayfield), you are required to provide [PickList.specialValues](#attr-picklistspecialvalues) as a map (there is no support for [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) automatically fetching appropriate display values).

Note that specialValues are not supported in conjunction with [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem). Whereas with [selectItem.multiple:true](SelectItem.md#attr-selectitemmultiple), specialValues will never be normal values that may be selected. So, specialValues should have options such as "Select All", "Select None" and others.

**Flags**: IR

---
## Attr: PickList.animatePickList

### Description
If true, when the pickList is shown, it will be shown via an animated reveal effect

### Groups

- pickList

**Flags**: IRWA

---
## Attr: PickList.showOptionsFromDataSource

### Description
If this item is part of a databound form, and has a specified `valueMap`, by default we show the valueMap options in the pickList for the item. Setting this property to true will ensure that the options displayed in our pickList are derived from the form's `dataSource`.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: PickList.pickListMaxWidth

### Description
Maximum width for this item's pickList. By default if the values displayed in this pickList are wider than the specified [PickList.pickListWidth](#attr-picklistpicklistwidth) the pickList will render wide enough to accommodate them. This property allows the developer to limit how wide the pickList will render.

### Groups

- pickList

**Flags**: IRW

---
## Attr: PickList.optionDataSource

### Description
If set, this FormItem will derive data to show in the PickList by fetching records from the specified `optionDataSource`. The fetched data will be used as a [valueMap](FormItem.md#attr-formitemvaluemap) by extracting the [valueField](FormItem.md#attr-formitemvaluefield) and [displayField](FormItem.md#attr-formitemdisplayfield) in the loaded records, to derive one valueMap entry per record loaded from the optionDataSource. Multiple fields from the fetched data may be shown in the pickList by setting [PickList.pickListFields](#attr-picklistpicklistfields).

The data will be retrieved via a "fetch" operation on the DataSource, passing the [PickList.pickListCriteria](#attr-picklistpicklistcriteria) (if set) as criteria, and passing [PickList.optionFilterContext](#attr-picklistoptionfiltercontext) (if set) as DSRequest Properties.

The fetch will be triggered when the pickList is first shown, or, you can set [autoFetchData:true](SelectItem.md#attr-selectitemautofetchdata) to fetch when the FormItem is first drawn.

The pickList will not re-fetch its options each time it is opened, unless the pickList criteria have changed. Developers who want to explicitly force a new fetch can achieve this by overriding [PickList.getPickListFilterCriteria](#method-picklistgetpicklistfiltercriteria) to dynamically generate criteria that change whenever appropriate. For example, to force a new fetch every time the pickList is shown, the generated criteria could include a subcriterion for some arbitrary field with _operator_ `notEqual` and _value_ set to a something that will change each time the method runs, such as a date-stamp.

Note that providing an initial value when [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) is enabled, or enabling [defaultToFirstOption](SelectItem.md#attr-selectitemdefaulttofirstoption), can also cause a fetch to be initiated immediately upon form creation. You can also call [PickList.fetchData](#method-picklistfetchdata) at any time to manually trigger a fetch.

Data paging is automatically enabled if the optionDataSource supports it. As the pickList is scrolled by the user, requests for additional data will be automatically issued.

For a pickList attached to a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem), new fetches are issued as the user types, with criteria set as described under [ComboBoxItem.getPickListFilterCriteria](ComboBoxItem.md#method-comboboxitemgetpicklistfiltercriteria). If your dataSource is not capable of filtering results by search criteria (eg, the dataSource is backed by an XML flat file), you can set [PickList.filterLocally](#attr-picklistfilterlocally) to have the entire dataset loaded up front and filtering performed in the browser. This disables data paging.

Note that if a normal, static [valueMap](FormItem.md#attr-formitemvaluemap) is **also** specified for the field (either directly in the form item or as part of the field definition in the dataSource), it will be preferred to the data derived from the optionDataSource for whatever mappings are present.

**Flags**: IRA

---
## Attr: PickList.displayField

### Description
If set, this item will display a value from another field to the user instead of showing the underlying data value for the [field name](FormItem.md#attr-formitemname).

This property is used in two ways:

The item will display the displayField value from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues) if [FormItem.useLocalDisplayFieldValue](FormItem.md#attr-formitemuselocaldisplayfieldvalue) is true, (or if unset and the conditions outlined in the documentation for that property are met).

If this field has an [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property is used by default to identify which value to use as a display value in records from this related dataSource. In this usage the specified displayField must be explicitly defined in the optionDataSource to be used - see [PickList.getDisplayFieldName](#method-picklistgetdisplayfieldname) for more on this behavior.  
If not using [local display values](#attr-picklistuselocaldisplayfieldvalue), the display value for this item will be derived by performing a fetch against the [option dataSource](FormItem.md#method-formitemgetoptiondatasource) to find a record where the [value field](FormItem.md#method-formitemgetvaluefieldname) matches this item's value, and use the `displayField` value from that record.  
In addition to this, PickList-based form items that provide a list of possible options such as the [SelectItem](SelectItem.md#class-selectitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) will show the `displayField` values to the user by default, allowing them to choose a new data value (see [FormItem.valueField](FormItem.md#attr-formitemvaluefield)) from a list of user-friendly display values.

This essentially allows the specified `optionDataSource` to be used as a server based [valueMap](../reference.md#kb-topic-valuemap).

If [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, selecting a new value will update both the value for this field and the associated display-field value on the record being edited.

Note: Developers may specify the [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) property in addition to `displayField`. This is useful for cases where the display field name in the local dataSource differs from the display field name in the optionDataSource. See the documentation for [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) for more on this.  
If a foreignDisplayField is specified, as with just displayField, if [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, when the user chooses a value the associated display-field value on the record being edited will be updated. In this case it would be set to the foreignDisplayField value from the related record. This means foreignDisplayField is always expected to be set to the equivalent field in the related dataSources.  
Developers looking to display some _other_ arbitrary field(s) from the related dataSource during editing should consider using custom [PickList.pickListFields](#attr-picklistpicklistfields) instead of setting a foreignDisplayField.

Note that if `optionDataSource` is set and no valid display field is specified, [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname) will return the dataSource title field by default.

If a displayField is specified for a freeform text based item (such as a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)), any user-entered value will be treated as a display value. In this scenario, items will derive the data value for the item from the first record where the displayField value matches the user-entered value. To avoid ambiguity, developers may wish to avoid this usage if display values are not unique.

### Groups

- databinding

### See Also

- [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname)
- [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

**Flags**: IRW

---
## Method: PickList.dataArrived

### Description
If this item is showing a dataBound pickList, this notification method will be fired when new data arrives from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | index of first row returned by the server |
| endRow | [int](../reference.md#type-int) | false | — | index of last row returned by the server |
| data | [ResultSet](#type-resultset) | false | — | pointer to this pickList's data |

---
## Method: PickList.getPickListFilterCriteria

### Description
[StringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview) to return a set of filter criteria to be applied to the data displayed in the pickList when it is shown.

If this is a databound item the criteria will be passed as criteria to [DataSource.fetchData](DataSource.md#method-datasourcefetchdata). Otherwise an equivalent client-side filter will be performed on the data returned by [PickList.getClientPickListData](#method-picklistgetclientpicklistdata).

By default combines [FormItem.optionCriteria](FormItem.md#attr-formitemoptioncriteria) with [PickList.pickListCriteria](#attr-picklistpicklistcriteria) if specified, otherwise an empty set of criteria so all records will be displayed.

Note that if no [optionCriteria](FormItem.md#attr-formitemoptioncriteria) are present and [pickListCriteria](#attr-picklistpicklistcriteria) were specified as a simple criteria object rather than an [AdvancedCriteria](../reference.md#object-advancedcriteria), the generated fetch operation to populate the pickList will contain these simple criteria (and [pickList.textMatchStyle](#attr-picklisttextmatchstyle) will determine how these criteria are interpreted).  
However if [optionCriteria](FormItem.md#attr-formitemoptioncriteria) are specified as a simple criteria object, an [AdvancedCriteria](../reference.md#object-advancedcriteria) object may be generated for the fetch even if pickListCriteria are not present, or also defined in simple criteria object format. See [PickList.useOptionTextMatchStyleInPickList](#attr-picklistuseoptiontextmatchstyleinpicklist) for details.

### Returns

`[Criteria](../reference_2.md#type-criteria)` — criteria to be used for databound or local filtering

**Flags**: A

---
## Method: PickList.getOptionDataSource

### Description
PickLists can derive their data directly from a valueMap, or retrieve data from a dataSource to display as options.

This method will return the dataSource used to populate the pickList, or null if none is specified (implies this list will derive its data from the valueMap for the item). Default implementation will return [PickList.optionDataSource](#attr-picklistoptiondatasource) if specified, otherwise if this is a field with a specified `foreignKey` in a databound form, returns the dataSource for the `foreignKey`. Otherwise picks up `this.form.dataSource` if set.

### Returns

`[DataSource](#type-datasource)` — DataSource to use for fetching options

---
## Method: PickList.getClientPickListData

### Description
Returns the set of data to be displayed in this item's PickList.

This method will be called for non-databound form items implementing the PickList interface. The default implementation will derive data from the item's valueMap - can be overridden to allow a custom set of options to be displayed.

Note that for PickLists that filter data based on user input ([ComboBox](ComboBoxItem.md#class-comboboxitem)), this method should return the data **before filtering**. To customize the data returned after filtering, override [PickList.filterClientPickListData](#method-picklistfilterclientpicklistdata) instead.

As an example, for a formItem with [PickList.valueField](#attr-picklistvaluefield) set to "valueFieldName", the default implementation would take a valueMap like the following:

```
     valueMap: { value1: "display 1", value2: "display 2" }
 
```
.. and returning the following set of records:
```
     [
          { valueFieldName : "value1" },
          { valueFieldName : "value2" }
     ]
 
```
Due to the valueMap, these records will appear as a two row pickList displayed as "display 1" and "display 2".

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — Array of record objects to be displayed in the pickList. Note that when a user picks a record from the list, the value of the field matching `item.valueField` will be picked. Also note that the fields to be displayed can be customized via `item.pickListFields`

**Flags**: A

---
## Method: PickList.getValueFieldName

### Description
Getter method to retrieve the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item. For items with a specified [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this determines which field in that dataSource corresponds to the value for this item.

If unset, if a [foreignKey relationship](DataSourceField.md#attr-datasourcefieldforeignkey) exists between this field and the optionDataSource, this will be used, otherwise default behavior will return the [FormItem.name](FormItem.md#attr-formitemname) of this field.

### Returns

`[String](#type-string)` — fieldName to use a "value field" in records from this items [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource)

### Groups

- display_values

---
## Method: PickList.fetchData

### Description
Only applies to databound items (see [PickList.optionDataSource](#attr-picklistoptiondatasource)).  
Performs a fetch type operation on this item's DataSource to retrieve the set of valid options for the item, based on the current [PickList.pickListCriteria](#attr-picklistpicklistcriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Callback to fire when the fetch completes. Callback will fire with 4 parameters:

*   `item` a pointer to the form item
*   `dsResponse` the [DSResponse](DSResponse.md#class-dsresponse) returned by the server
*   `data` the raw data returned by the server
*   `dsRequest` the [DSRequest](../reference.md#object-dsrequest) sent to the server |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | properties to apply to the dsRequest for this fetch. |

---
## Method: PickList.getDisplayFieldName

### Description
Returns the `displayField` for this item.

Behavior varies based on the configuration of this item, as follows:

*   If this item has an [PickList.optionDataSource](#attr-picklistoptiondatasource) and an explicit [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) is specified, this will be returned.
*   Otherwise if an explicit [PickList.displayField](#attr-picklistdisplayfield) is specified it will be returned by default. If the `displayField` was specified on the underlying dataSource field, and no matching field is present in the [PickList.optionDataSource](#attr-picklistoptiondatasource) for the item, we avoid returning the specified displayField value and instead return the title field of the option DataSource. We do this to avoid confusion for the case where the displayField is intended as a display-field value for showing another field value within the same record in the underlying dataSource only.
*   If no explicit foreignDisplay or displayField specification was found, and the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item is hidden in the [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this method will return the title field for the `optionDataSource`.

### Returns

`[FieldName](../reference.md#type-fieldname)` — display field name, or null if there is no separate display field to use.

---
## Method: PickList.filterClientPickListData

### Description
Returns the data to display in the pick list.

The default implementation applies the criteria returned by [PickList.getPickListFilterCriteria](#method-picklistgetpicklistfiltercriteria) to the data returned by [PickList.getClientPickListData](#method-picklistgetclientpicklistdata). A record passes the filter if it has a matching value for all fields in the criteria object. Matching is performed according to [TextMatchStyle](../reference.md#type-textmatchstyle).

If [PickList.showAllOptions](#attr-picklistshowalloptions) is set, all values are shown, with matching values shown below a [separator](#attr-picklistseparatorrows).

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — array of record objects to display in the pickList

---
