# SelectItem Documentation

[← Back to API Index](../main.md)

---

## Class: SelectItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
FormItem that allows picking between several mutually exclusive options via a select list.

Options may be derived from a `dataSource` or a `valueMap`.

Note that to select the first option as a default value for the item, [SelectItem.defaultToFirstOption](#attr-selectitemdefaulttofirstoption) may be set.

### See Also

- [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)
- [FormItem.valueMap](FormItem.md#attr-formitemvaluemap)

---
## Attr: SelectItem.fetchDisplayedFieldsOnly

### Description
If this item has a specified `optionDataSource` and this property is `true`, the list of fields used by this pickList will be passed to the datasource as [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs). If the datasource supports this feature the returned fields will be limited to this list. A custom datasource will need to add code to implement field limiting.

This list of used fields consists of the values of [valueField](FormItem.md#attr-formitemvaluefield), [displayField](FormItem.md#attr-formitemdisplayfield) and [pickListFields](#attr-selectitempicklistfields).

NOTE: When enabled, [getSelectedRecord](FormItem.md#method-formitemgetselectedrecord) will only include the fetched fields.

**Flags**: IRA

---
## Attr: SelectItem.showFocused

### Description
When this item receives focus, should it be re-styled to indicate it has focus?

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for more details on formItem styling.

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](FormItem.md#attr-formitemcellstyle)

**Flags**: IRWA

---
## Attr: SelectItem.pickerExitButtonTitle

### Description
The title for the [SelectItem.pickerExitButton](#attr-selectitempickerexitbutton).

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: SelectItem.pickButtonWidth

### Description
How large should the pick button be rendered?

**Deprecated**

**Flags**: IRWA

---
## Attr: SelectItem.pickListFields

### Description
This property allows the developer to specify which field\[s\] will be displayed in the drop down list of options.

Only applies to databound pickLists (see [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource), or pickLists with custom data set up via the advanced [PickList.getClientPickListData](PickList.md#method-picklistgetclientpicklistdata) method.

If this property is unset, we display the [PickList.displayField](PickList.md#attr-picklistdisplayfield), if specified, otherwise the [PickList.valueField](PickList.md#attr-picklistvaluefield).

If there are multiple fields, column headers will be shown for each field, the height of which can be customized via the [PickList.pickListHeaderHeight](PickList.md#attr-picklistpicklistheaderheight) attribute.

Each field to display should be specified as a [ListGridField](../main_2.md#object-listgridfield) object. Note that unlike in [listGrids](ListGrid_1.md#class-listgrid), dataSource fields marked as [hidden:true](DataSourceField.md#attr-datasourcefieldhidden) will be hidden by default in pickLists. To override this behavior, ensure that you specify an explicit value for [showIf](ListGridField.md#method-listgridfieldshowif).

### Groups

- pickList

### See Also

- [SelectItem.valueField](#attr-selectitemvaluefield)
- [PickList.pickListHeaderHeight](PickList.md#attr-picklistpicklistheaderheight)

**Flags**: IRA

---
## Attr: SelectItem.filterLocally

### Description
If `filterLocally` is set for this item, and this item is showing options from a dataSource, fetch the entire set of options from the server, and use these values to map the item value to the appropriate display value. Also use `"local"` type filtering on drop down list of options.

This means data will only be fetched once from the server, and then filtered on the client.

Note - when this property is set to `false`, filtering will still be performed on the client if a complete set of data for some criteria has been cached by a fetch, and a subsequent fetch has more restrictive criteria. To explicitly disable client-side filtering set the [SelectItem.useClientFiltering](#attr-selectitemuseclientfiltering) property to false.

### See Also

- [FormItem.filterLocally](FormItem.md#attr-formitemfilterlocally)

**Flags**: IRA

---
## Attr: SelectItem.pickerNavigationBar

### Description
[NavigationBar](NavigationBar.md#class-navigationbar) created when [SelectItem.pickListPlacement](#attr-selectitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: SelectItem.showHintInField

### Description
If showing a hint for this form item, should it be shown within the field?

CSS style for the hint is [SelectItem.textBoxStyle](#attr-selectitemtextboxstyle) with the suffix "Hint" appended to it.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)

**Flags**: IRW

---
## Attr: SelectItem.optionFilterContext

### Description
If this item has a specified `optionDataSource`, and this property is not null, this will be passed to the datasource as [DSRequest](../main_2.md#object-dsrequest) properties when performing the filter operation on the dataSource to obtain the set of options for the list. This provides, among other capabilities, a way to trigger the server to return summary records.

### See Also

- [serverSummaries](../kb_topics/serverSummaries.md#kb-topic-server-summaries)

**Flags**: IRA

---
## Attr: SelectItem.pickerClearButtonTitle

### Description
The title for the [SelectItem.pickerClearButton](#attr-selectitempickerclearbutton).

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: SelectItem.pickButtonSrc

### Description
Source for image to show for the pick button

**Deprecated**

**Flags**: IRWA

---
## Attr: SelectItem.valueField

### Description
If this form item maps data values to display values by retrieving the [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) values from an [optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property denotes the the field to use as the underlying data value in records from the optionDataSource.  
If not explicitly supplied, the valueField name will be derived as described in [FormItem.getValueFieldName](FormItem.md#method-formitemgetvaluefieldname).

### Groups

- databinding

**Flags**: IRW

---
## Attr: SelectItem.cachePickListResults

### Description
For databound pickLists (see [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)), by default SmartClient will cache and re-use datasets shown by pickLists in an LRU (least recently used) caching pattern.

Setting this flag to false avoids this caching for situations where it is too aggressive.

**Flags**: IR

---
## Attr: SelectItem.textBoxStyle

### Description
Base CSS class name for a form item's text box element.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for an overview of formItem styling, and the [CompoundFormItem_skinning](../main.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

If the `textBoxStyle` is changed at runtime, [updateState()](FormItem.md#method-formitemupdatestate) must be called to update the visual state of this item.

### Groups

- appearance

### See Also

- [FormItem.cellStyle](FormItem.md#attr-formitemcellstyle)

**Flags**: IRA

---
## Attr: SelectItem.pickListPlacement

### Description
Controls where the [PickList](../main_2.md#interface-picklist) is placed. Can be specified as a [PanelPlacement](../main_2.md#type-panelplacement) or a specific widget that should be filled (by specifying an actual Canvas or [Canvas.ID](Canvas.md#attr-canvasid)).

Default behavior is to `"fillPanel"` if [Browser.isHandset](Browser.md#classattr-browserishandset) or [Browser.isTablet](Browser.md#classattr-browseristablet), to better accommodate the smaller screen real estate and less precise pointing ability on such devices.

When filling the whole screen, part of the screen or a specific panel, the expanded interface is created as a [standard FormItem picker](FormItem.md#attr-formitempicker), and incorporates a [navigation bar](#attr-selectitempickernavigationbar) and [done button](#attr-selectitempickerexitbutton) that hides the expanded interface.

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: SelectItem.addUnknownValues

### Description
If this item's value is set (via [SelectItem.setValue](#method-selectitemsetvalue) or similar) to a value which is not present in the [ValueMap](../main_2.md#type-valuemap), should the value be rejected.

If set to `false` the setValue() call will have no effect if the value is not a valid option.

If set to `true` the item's value will be updated to the new value, and the value will be added to the set of options displayed in the pick-list until the next call to [SelectItem.setValueMap](#method-selectitemsetvaluemap) or [SelectItem.setValue](#method-selectitemsetvalue).

Exception: If the value is set to `null` but there is no null entry in the valueMap for this item, setting `addUnknownValues` to true will not cause a null option to show up at the top of the select item pickList. Whether an empty option is shown in the pickList is governed by [SelectItem.allowEmptyValue](#attr-selectitemallowemptyvalue) instead.

Note that this property has no effect if the selectItem has a specified [SelectItem.optionDataSource](#attr-selectitemoptiondatasource). If [SelectItem.setValue](#method-selectitemsetvalue) is called on a databound SelectItem and the new value does not match any loaded options, the value will be accepted, but not added to the options displayed in the pickList. Also note that if a [SelectItem.displayField](#attr-selectitemdisplayfield) exists, a fetch will be performed in an attempt to retrieve a valid display value, as described under [FormItem.fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues). If specified the [FormItem.loadingDisplayValue](FormItem.md#attr-formitemloadingdisplayvalue) will be displayed while the fetch is in progress, and then the real value (mapped to a display field value if a matching record was found) will be displayed when the fetch completes.

**Flags**: IRWA

---
## Attr: SelectItem.dataSetType

### Description
Whether to show the picker as a flat list, or a collapsible tree.

The default value, "list", will use an instance of the [pickListConstructor](PickList.md#attr-picklistpicklistconstructor) as the picker - "tree" will show an instance of [pickTreeConstructor](PickList.md#attr-picklistpicktreeconstructor).

**Flags**: IR

---
## Attr: SelectItem.openOnSpace

### Description
Causes the PickList to open when the spacebar is pressed, default false.

For native OS widgets, space opens the PickList on Macs, but not on Windows. Consider using this setting if your users are almost entirely Mac users, or enabling it only for users running MacOS.

However, before using this setting, consider that it means that Spacebar will not be able to be used for another purpose when focus is in a SelectItem.

**Flags**: IRW

---
## Attr: SelectItem.rootNodeId

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), this is the [id](#attr-selectitemvaluefield) of the record to use as the [root](Tree.md#attr-treerootvalue) node.

**Flags**: IRW

---
## Attr: SelectItem.hiliteTextColor

### Description
Text color to apply to the select item's selected value when the SelectItem receives focus, if `hiliteOnFocus` is true.

**Deprecated**

**Flags**: IRWA

---
## Attr: SelectItem.initialSort

### Description
An array of [SortSpecifier](../main_2.md#object-sortspecifier) objects used to set up the initial sort configuration for this pickList. If specified, this will be used instead of any [PickList.sortField](PickList.md#attr-picklistsortfield) specified.

### Groups

- sorting

**Flags**: IR

---
## Attr: SelectItem.singleClickFolderToggle

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), the default behavior is for folder open-state to be toggled by double-clicking. Set this attribute to true to toggle folders on a single-click instead.

Note: when set to true, users can only choose leaf-nodes, since clicking folders would simply toggle them.

**Flags**: IRW

---
## Attr: SelectItem.defaultToFirstOption

### Description
Select the first option as the default value for this SelectItem.

If options are derived from a dataSource, the first value returned by the server will be used, otherwise the first value in the valueMap. Note that setting this property to true will trigger a fetch at soon as the form is created, because the form will try to establish a default value at that time.

If enabled, this setting overrides [SelectItem.defaultValue](#attr-selectitemdefaultvalue) and [SelectItem.defaultDynamicValue](#method-selectitemdefaultdynamicvalue).

### Groups

- formValues

**Flags**: IRW

---
## Attr: SelectItem.escapeHTML

### Description
By default HTML values in a selectItem will be interpreted by the browser. Setting this flag to true will causes HTML characters to be escaped, meaning the raw value of the field (for example `"`<b>`AAA`</b>`"`) is displayed to the user rather than the interpreted HTML (for example `"**AAA**"`)

### Groups

- appearance

**Flags**: IRW

---
## Attr: SelectItem.pickerIconWidth

### Description
If [showPickerIcon](#attr-selectitemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../main.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: SelectItem.hiliteColor

### Description
Background color to apply to the select item's selected value when the SelectItem receives focus, if `hiliteOnFocus` is true.

**Deprecated**

**Flags**: IRWA

---
## Attr: SelectItem.pickerClearButton

### Description
[NavigationButton](NavigationButton.md#class-navigationbutton) to clear the picker value, created when [SelectItem.pickListPlacement](#attr-selectitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

This button will only be shown if [SelectItem.allowEmptyValue](#attr-selectitemallowemptyvalue) is true.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pickerClearButtonTitle](#attr-selectitempickerclearbuttontitle) for [Button.title](Button.md#attr-buttontitle)

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: SelectItem.optionDataSource

### Description
If set, this FormItem will derive data to show in the PickList by fetching records from the specified `optionDataSource`. The fetched data will be used as a [valueMap](FormItem.md#attr-formitemvaluemap) by extracting the [valueField](FormItem.md#attr-formitemvaluefield) and [displayField](FormItem.md#attr-formitemdisplayfield) in the loaded records, to derive one valueMap entry per record loaded from the optionDataSource. Multiple fields from the fetched data may be shown in the pickList by setting [SelectItem.pickListFields](#attr-selectitempicklistfields).

The data will be retrieved via a "fetch" operation on the DataSource, passing the [PickList.pickListCriteria](PickList.md#attr-picklistpicklistcriteria) (if set) as criteria, and passing [SelectItem.optionFilterContext](#attr-selectitemoptionfiltercontext) (if set) as DSRequest Properties.

The fetch will be triggered when the pickList is first shown, or, you can set [autoFetchData:true](#attr-selectitemautofetchdata) to fetch when the FormItem is first drawn.

The pickList will not re-fetch its options each time it is opened, unless the pickList criteria have changed. Developers who want to explicitly force a new fetch can achieve this by overriding [PickList.getPickListFilterCriteria](PickList.md#method-picklistgetpicklistfiltercriteria) to dynamically generate criteria that change whenever appropriate. For example, to force a new fetch every time the pickList is shown, the generated criteria could include a subcriterion for some arbitrary field with _operator_ `notEqual` and _value_ set to a something that will change each time the method runs, such as a date-stamp.

Note that providing an initial value when [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) is enabled, or enabling [defaultToFirstOption](#attr-selectitemdefaulttofirstoption), can also cause a fetch to be initiated immediately upon form creation. You can also call [PickList.fetchData](PickList.md#method-picklistfetchdata) at any time to manually trigger a fetch.

Data paging is automatically enabled if the optionDataSource supports it. As the pickList is scrolled by the user, requests for additional data will be automatically issued.

For a pickList attached to a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem), new fetches are issued as the user types, with criteria set as described under [ComboBoxItem.getPickListFilterCriteria](ComboBoxItem.md#method-comboboxitemgetpicklistfiltercriteria). If your dataSource is not capable of filtering results by search criteria (eg, the dataSource is backed by an XML flat file), you can set [SelectItem.filterLocally](#attr-selectitemfilterlocally) to have the entire dataset loaded up front and filtering performed in the browser. This disables data paging.

Note that if a normal, static [valueMap](FormItem.md#attr-formitemvaluemap) is **also** specified for the field (either directly in the form item or as part of the field definition in the dataSource), it will be preferred to the data derived from the optionDataSource for whatever mappings are present.

**Flags**: IR

---
## Attr: SelectItem.pickerExitButton

### Description
[NavigationButton](NavigationButton.md#class-navigationbutton) to dismiss the picker interface, created when [SelectItem.pickListPlacement](#attr-selectitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pickerExitButtonTitle](#attr-selectitempickerexitbuttontitle) for [Button.title](Button.md#attr-buttontitle)

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: SelectItem.iconPlacement

### Description
For PickList items with [PickListItemIconPlacement](../main.md#type-picklistitemiconplacement) set such that the pickList does not render near-origin, should specified [icons](FormItem.md#attr-formitemicons) be rendered inline within the formItem itself, or within the [pickerNavigationBar](ComboBoxItem.md#attr-comboboxitempickernavigationbar).

May be overridden at the icon level via [FormItemIcon.iconPlacement](FormItemIcon.md#attr-formitemiconiconplacement).

For mobile browsing with limited available screen space, icons rendered in the navigation bar may be easier for the user to interact with.

**Flags**: IR

---
## Attr: SelectItem.showOptionsFromDataSource

### Description
If this item is part of a databound form, and has a specified `valueMap`, by default we show the valueMap options in the pickList for the item. Setting this property to true will ensure that the options displayed in our pickList are derived from the form's `dataSource`.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: SelectItem.multipleAppearance

### Description
How should items with [SelectItem.multiple](#attr-selectitemmultiple) set to 'true' be displayed?

**Flags**: IR

---
## Attr: SelectItem.controlStyle

### Description
Base CSS class name for a form item's "control box". This is an HTML element which contains the text box and picker icon for the item.

See [FormItem.alwaysShowControlBox](FormItem.md#attr-formitemalwaysshowcontrolbox) for details on when the control box is written out.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for an overview of formItem styling, and the [CompoundFormItem_skinning](../main.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

### Groups

- appearance

### See Also

- [FormItem.cellStyle](FormItem.md#attr-formitemcellstyle)

**Flags**: IRA

---
## Attr: SelectItem.updateControlOnOver

### Description
If [FormItem.showOver](FormItem.md#attr-formitemshowover) is true, setting this property to false will explicitly disable showing the "Over" state for the control table element of this item (if present).

### Groups

- formItemStyling

### See Also

- [SelectItem.showOver](#attr-selectitemshowover)

**Flags**: IRWA

---
## Attr: SelectItem.pickTreeConstructor

### Description
The Class to use when creating a picker of [type "tree"](PickList.md#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickTreeMenu](../main.md#class-picktreemenu).

**Flags**: IR

---
## Attr: SelectItem.pickList

### Description
ListGrid-based AutoChild created by the system to display a list of pickable options for this item.

The pickList is automatically generated and displayed by the system when necessary. It may be customized via properties such as [SelectItem.pickListConstructor](#attr-selectitempicklistconstructor), [SelectItem.pickTreeConstructor](#attr-selectitempicktreeconstructor), [SelectItem.pickListProperties](#attr-selectitempicklistproperties) and more. See the [PickList overview](../main_2.md#interface-picklist) for more information.

Accessing the generated pickList at runtime is an advanced usage. In most cases developers should not modify this generated component directly but should instead use attributes on the formItem to configure it.

**Flags**: RA

---
## Attr: SelectItem.saveOnEnter

### Description
Select items will submit their containing form on enter keypress if [saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) is true. Setting this property to `false` will disable this behavior.

Note that if the drop down list of options (pickList) is visible an `Enter` keypress is used to select a value from the available set of options and will not automatically cause form submission.

**Flags**: IRW

---
## Attr: SelectItem.autoFetchData

### Description
If this select item retrieves its options from a `dataSource`, should options be fetched from the server when the item is first drawn, or should this fetch be delayed until the user opens the pickList.

The default is true in order to allow the user to select a value via keyboard input while keyboard focus is on the SelectItem but the pickList has not actually been shown.

### See Also

- [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)

**Flags**: IRA

---
## Attr: SelectItem.pickListProperties

### Description
If specified this properties block will be applied to the [pickList](PickListMenu.md#class-picklistmenu) created for this FormItem.

_Note_: Not every ListGrid property is supported when assigned to a pickList. Where there is a dedicated API on the form item (such as [pickListCellHeight](PickList.md#attr-picklistpicklistcellheight)), we recommend that be used in favor of setting the equivalent property on the `pickListProperties` block.

_PickLists and [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor):_  
[ComboBoxItems](ComboBoxItem.md#class-comboboxitem) do not support setting `showFilterEditor` to true on pickListProperties. This combination of settings leads to an ambiguous user experience as the two sets of filter-criteria (those from the text-box and those from the pickList filter editor) interact with each other.  
Setting [showFilterEditor:true](ListGrid_1.md#attr-listgridshowfiltereditor) in [SelectItem.pickListProperties](#attr-selectitempicklistproperties) is a valid way to create a filterable pickList, on a SelectItem, but this setting is not supported on a SelectItem with [SelectItem.multiple](#attr-selectitemmultiple) set to true - this combination of settings can cause a selected value to be filtered out of view at which point further selection changes will discard that value.  
In general we recommend the ComboBoxItem class (with [ComboBoxItem.addUnknownValues](ComboBoxItem.md#attr-comboboxitemaddunknownvalues) set as appropriate) as a better interface for filtering pickList data.

### Groups

- pickList

**Flags**: IRA

---
## Attr: SelectItem.pickerIconStyle

### Description
Base CSS class name for a form item's picker icon cell. If unset, inherits from this item's [controlStyle](#attr-selectitemcontrolstyle).

### Groups

- pickerIcon
- formItemStyling

### See Also

- [FormItem.cellStyle](FormItem.md#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: SelectItem.pickListCriteria

### Description
If this item has a databound pickList (for example [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource) is set), this property can be used to provide static filter criteria when retrieving the data for the pickList.

### Groups

- pickList

**Flags**: IRWA

---
## Attr: SelectItem.progressiveLoading

### Description
Indicates whether or not this SelectItem will load its list of options [progressively](DataSource.md#attr-datasourceprogressiveloading). This property is copied onto the underlying [PickList](../main_2.md#interface-picklist).

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)

**Flags**: IRW

---
## Attr: SelectItem.defaultValue

### Description
Static default value for this SelectItem. To default to the first option use [SelectItem.defaultToFirstOption](#attr-selectitemdefaulttofirstoption) instead.

**Flags**: IRW

---
## Attr: SelectItem.displayField

### Description
If set, this item will display a value from another field to the user instead of showing the underlying data value for the [field name](FormItem.md#attr-formitemname).

This property is used in two ways:

The item will display the displayField value from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues) if [FormItem.useLocalDisplayFieldValue](FormItem.md#attr-formitemuselocaldisplayfieldvalue) is true, (or if unset and the conditions outlined in the documentation for that property are met).

If this field has an [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property is used by default to identify which value to use as a display value in records from this related dataSource. In this usage the specified displayField must be explicitly defined in the optionDataSource to be used - see [SelectItem.getDisplayFieldName](#method-selectitemgetdisplayfieldname) for more on this behavior.  
If not using [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue), the display value for this item will be derived by performing a fetch against the [option dataSource](FormItem.md#method-formitemgetoptiondatasource) to find a record where the [value field](FormItem.md#method-formitemgetvaluefieldname) matches this item's value, and use the `displayField` value from that record.  
In addition to this, PickList-based form items that provide a list of possible options such as the [SelectItem](#class-selectitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) will show the `displayField` values to the user by default, allowing them to choose a new data value (see [FormItem.valueField](FormItem.md#attr-formitemvaluefield)) from a list of user-friendly display values.

This essentially allows the specified `optionDataSource` to be used as a server based [valueMap](../main.md#kb-topic-valuemap).

If [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, selecting a new value will update both the value for this field and the associated display-field value on the record being edited.

Note: Developers may specify the [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) property in addition to `displayField`. This is useful for cases where the display field name in the local dataSource differs from the display field name in the optionDataSource. See the documentation for [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) for more on this.  
If a foreignDisplayField is specified, as with just displayField, if [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, when the user chooses a value the associated display-field value on the record being edited will be updated. In this case it would be set to the foreignDisplayField value from the related record. This means foreignDisplayField is always expected to be set to the equivalent field in the related dataSources.  
Developers looking to display some _other_ arbitrary field(s) from the related dataSource during editing should consider using custom [PickList.pickListFields](PickList.md#attr-picklistpicklistfields) instead of setting a foreignDisplayField.

Note that if `optionDataSource` is set and no valid display field is specified, [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname) will return the dataSource title field by default.

If a displayField is specified for a freeform text based item (such as a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)), any user-entered value will be treated as a display value. In this scenario, items will derive the data value for the item from the first record where the displayField value matches the user-entered value. To avoid ambiguity, developers may wish to avoid this usage if display values are not unique.

### Groups

- databinding

### See Also

- [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname)
- [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

**Flags**: IRW

---
## Attr: SelectItem.sortField

### Description
Specifies one or more fields by which this item should be initially sorted. It can be a [field name](ListGridField.md#attr-listgridfieldname), or an array of field names - but note that, if multiple fields are supplied, then each will be sorted in the same [direction](ListGrid_1.md#attr-listgridsortdirection).

For full sorting control, set [initialSort](PickList.md#attr-picklistinitialsort) to a list of custom [sortSpecifiers](../main_2.md#object-sortspecifier).

This attribute can also be set to the index of a field in the fields array, but note that it will be converted to a string (field name) after initialization.

### Groups

- sorting

**Flags**: IR

---
## Attr: SelectItem.canSelectText

### Description
By default SelectItems do not allow users to select the text of the selected value.

**Flags**: IRW

---
## Attr: SelectItem.specialValues

### Description
A set of "special" values such as "All", "None" or "Invalid" that do not appear in the normal [ValueMap](../main_2.md#type-valuemap) or in the data returned by the [SelectItem.optionDataSource](#attr-selectitemoptiondatasource).

Like other uses of [ValueMap](../main_2.md#type-valuemap), either a list of values or a mapping from stored to display value can be provided.

These values can either be shown at the top of the list of values (in the order specified), or can be shown in a separate, non-scrolling region - the setting [separateSpecialValues](#attr-selectitemseparatespecialvalues) controls this. Note that data paging can only be used if `separateSpecialValues` is enabled.

If `specialValues` are configured, [allowEmptyValue](#attr-selectitemallowemptyvalue) is ignored - an empty value, if desired, must be included in the `specialValues`. To provide a `specialValue` which clears the value of the field, use the special constant [PickList.emptyStoredValue](PickList.md#classattr-picklistemptystoredvalue).

`specialValues` can also be used to take a value that _does_ appear in the normal data and redundantly display it at the top of the list to make it more accessible. Note that in this case it is expected that the special value appears _both_ at the top of the list _and_ in it's normal position in the list, so this works best with [separateSpecialValues](#attr-selectitemseparatespecialvalues) mode enabled.

Also, if an [SelectItem.optionDataSource](#attr-selectitemoptiondatasource) is used, [SelectItem.specialValues](#attr-selectitemspecialvalues) that appear in the normal dataset _will_ be updated by automatic [cache synchronization](../main.md#kb-topic-cachesync) (if the [SelectItem.displayField](#attr-selectitemdisplayfield) is updated). However when using a distinct [SelectItem.valueField](#attr-selectitemvaluefield) and [SelectItem.displayField](#attr-selectitemdisplayfield), you are required to provide [SelectItem.specialValues](#attr-selectitemspecialvalues) as a map (there is no support for [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) automatically fetching appropriate display values).

Note that specialValues are not supported in conjunction with [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem). Whereas with [selectItem.multiple:true](#attr-selectitemmultiple), specialValues will never be normal values that may be selected. So, specialValues should have options such as "Select All", "Select None" and others.

**Flags**: IR

---
## Attr: SelectItem.allowEmptyValue

### Description
If set to true, always show an empty option in this item's pickList, allowing the user to clear the value (even if there is no empty entry in the valueMap for the item).

The empty value will be displayed with the [emptyDisplayValue](FormItem.md#attr-formitememptydisplayvalue).

With a [databound selectItem](#attr-selectitemoptiondatasource), enabling `allowEmptyValue` disables data paging by default - all data matching the [current criteria](PickList.md#attr-picklistpicklistcriteria) will be requested. However, enabling [SelectItem.separateSpecialValues](#attr-selectitemseparatespecialvalues) allows data paging to be used if required.

See also [SelectItem.specialValues](#attr-selectitemspecialvalues) as a way of providing several different special values in addition to an empty value, such as "Invalid". Note that setting `specialValues` disables the use of `allowEmptyValue` - see details of how to have an empty value while using `specialValues` in in [the `specialValues` documentation](#attr-selectitemspecialvalues).

### Groups

- formValues

**Flags**: IR

---
## Attr: SelectItem.height

### Description
Height of the FormItem. Can be either a number indicating a fixed height in pixels, a percentage indicating a percentage of the overall form's height, or "\*" indicating take whatever remaining space is available. See the [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout) overview for details.

For form items having a [picker icon](#attr-selectitemshowpickericon) (e.g. [SelectItem](#class-selectitem), [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)) and [SpinnerItem](SpinnerItem.md#class-spinneritem)s, if there is no explicit [FormItem.pickerIconHeight](FormItem.md#attr-formitempickericonheight), the pickerIcon will be sized to match the available space based on the specified item height.  
Note that if spriting is being used, and the image to be displayed in these icons is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../main.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.  
Alternatively, the [pickerIconStyle](#attr-selectitempickericonstyle) could be changed to a custom CSS style name, and in the case of [SpinnerItem](SpinnerItem.md#class-spinneritem)s, the [baseStyle](FormItemIcon.md#attr-formitemiconbasestyle) and [src](FormItemIcon.md#attr-formitemiconsrc) of the [SpinnerItem.increaseIcon](SpinnerItem.md#attr-spinneritemincreaseicon) and [SpinnerItem.decreaseIcon](SpinnerItem.md#attr-spinneritemdecreaseicon) AutoChildren could be customized.

Note that when FormItem is rendered as read-only with `readOnlyDisplay` as "static" the property [FormItem.staticHeight](FormItem.md#attr-formitemstaticheight) is used instead.

### Groups

- formLayout

### See Also

- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)
- [FormItem.width](FormItem.md#attr-formitemwidth)
- [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout)

**Flags**: IRW

---
## Attr: SelectItem.pickListConstructor

### Description
The Class to use when creating a picker of [type "list"](PickList.md#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickListMenu](PickListMenu.md#class-picklistmenu).

### Groups

- pickList

**Flags**: IR

---
## Attr: SelectItem.updateTextBoxOnOver

### Description
If [FormItem.showOver](FormItem.md#attr-formitemshowover) is true, setting this property to false will explicitly disable showing the "Over" state for the TextBox element of this item.

### Groups

- formItemStyling

### See Also

- [SelectItem.showOver](#attr-selectitemshowover)

**Flags**: IRWA

---
## Attr: SelectItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: SelectItem.useClientFiltering

### Description
For [databound](#attr-selectitemoptiondatasource) items, this property will be passed to the generated ResultSet data object for the pickList as [ResultSet.useClientFiltering](ResultSet.md#attr-resultsetuseclientfiltering). Setting to false will disable filtering on the client and ensure criteria are always passed to the DataSource directly.

**Flags**: IRA

---
## Attr: SelectItem.clickMaskMode

### Description
Determines the behavior of the click-mask thrown up when this pickList is visible.

The default value, "hard", matches the familiar behavior of combos and selects on Windows, Mac and other platforms - mouse-events such as rollovers are blocked and, when a click is received, the picker is hidden and the event is cancelled.

When `clickMaskMode` is "soft", mouse-events continue to fire, meaning that rollover styles, for example, continue to be updated. When a click is received in this mode, the picker is hidden and the click event is allowed to proceed to its target - this means that clicking an item with an open picker will re-open the picker.

**Flags**: IRW

---
## Attr: SelectItem.optionOperationId

### Description
If this item has a specified `optionDataSource`, this attribute may be set to specify an explicit [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) when performing a fetch against the option dataSource to pick up display value mapping.

### Groups

- databinding

**Flags**: IR

---
## Attr: SelectItem.emptyDisplayValue

### Description
Text to display when this form item has a null or undefined value.

If the formItem has a databound pickList, and its [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) or [FormItem.valueField](FormItem.md#attr-formitemvaluefield) (if the former isn't set) has an undefined [emptyCellValue](ListGridField.md#attr-listgridfieldemptycellvalue) setting, that field's `emptyCellValue` will automatically be set to the `emptyDisplayValue`.

### Groups

- display_values

**Flags**: IRW

---
## Attr: SelectItem.emptyPickListMessage

### Description
Empty message to display in the selectItem if [PickList.hideEmptyPickList](PickList.md#attr-picklisthideemptypicklist) is `false`.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: SelectItem.textMatchStyle

### Description
When applying filter criteria to pickList data, what type of matching to use.

For a databound pickList ([SelectItem.optionDataSource](#attr-selectitemoptiondatasource) set), `textMatchStyle` is sent to the server as [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle).

For a non-databound pickList, `textMatchStyle` is applied by [filterClientPickListData()](PickList.md#method-picklistfilterclientpicklistdata).

**Flags**: IR

---
## Attr: SelectItem.separateValuesList

### Description
AutoChild used to show [SelectItem.specialValues](#attr-selectitemspecialvalues).

**Flags**: IR

---
## Attr: SelectItem.separateSpecialValues

### Description
If true, [special values](#attr-selectitemspecialvalues) such as the empty value will be shown in a separate non-scrolling area, in the [SelectItem.separateValuesList](#attr-selectitemseparatevalueslist). Aside from making these values more easily accessible, showing them in a separate list allows data paging to be used, which is disabled if the separateValues are shown in the normal drop-down list along with other values.

**Flags**: IR

---
## Attr: SelectItem.pickerIconHeight

### Description
If [showPickerIcon](#attr-selectitemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../main.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: SelectItem.showPickerIcon

### Description
Should we show a special 'picker' [icon](../main.md#object-formitemicon) for this form item? Picker icons are customizable via [pickerIconProperties](FormItem.md#attr-formitempickericonproperties). By default they will be rendered inside the form item's ["control box"](FormItem.md#attr-formitemcontrolstyle) area. By default clicking the pickerIcon will call [FormItem.showPicker](FormItem.md#method-formitemshowpicker).

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: SelectItem.allowMultiCharSearch

### Description
By default, if multiple keys are pressed in quick succession, a SelectItem will buffer them together and use the resulting multi-char string when searching. Set this attribute to false to force the item to match only one character at a time.

**Flags**: IRW

---
## Attr: SelectItem.openOnDownArrow

### Description
Causes the PickList to open when the down arrow is pressed, default false.

For native OS widgets, the down arrow changes the value of a select on Windows, but opens the select on Macs. This setting is not recommended unless you are certain that all users of your applications will expect the Mac convention.

**Flags**: IRW

---
## Attr: SelectItem.pickerIconSrc

### Description
If [showPickerIcon](#attr-selectitemshowpickericon) is true for this item, this property governs the [src](FormItemIcon.md#attr-formitemiconsrc) of the picker icon image to be displayed.

When [spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) is enabled, this property will not be used to locate an image, instead, the image is drawn via CSS based on the [SelectItem.pickerIconStyle](#attr-selectitempickericonstyle) property.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: SelectItem.hiliteOnFocus

### Description
Should this SelectItem show a hilite when it receives keyboard focus?

**Deprecated**

**Flags**: IRWA

---
## Attr: SelectItem.showOver

### Description
When the user rolls over this item, should it be re-styled to indicate it has focus?

By default this property is true for SelectItems, and [SelectItem.updateTextBoxOnOver](#attr-selectitemupdatetextboxonover) and [SelectItem.updateControlOnOver](#attr-selectitemupdatecontrolonover) are set to false. This means the picker icon will show over styling when the user rolls over the control table.  
These defaults may be overridden by different SmartClient skins.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for more details on formItem styling.

### Groups

- formItemStyling

**Flags**: IRWA

---
## Attr: SelectItem.pickButtonHeight

### Description
How large should the pick button be rendered?

**Deprecated**

**Flags**: IRWA

---
## Attr: SelectItem.autoOpenTree

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), which nodes should be opened automatically. Options are:

*   "none" - no nodes are opened automatically
*   "root" - opens the [top-level node](PickList.md#attr-picklistrootnodeid) - in databound tree-pickers, this node is always hidden
*   "all" - when [loading data on demand](ResultTree.md#attr-resulttreeloaddataondemand), opens the [top-level node](PickList.md#attr-picklistrootnodeid) and all of it's direct descendants - otherwise, opens all loaded nodes

**Flags**: IRW

---
## Attr: SelectItem.multiple

### Description
If true, multiple values may be selected.

The SelectItem will either render as a drop-down allowing multiple selections, or a multi-row list of options similar to a small headerless [ListGrid](ListGrid_1.md#class-listgrid), based on the [MultipleAppearance](../main.md#type-multipleappearance) setting.

The logical value of the formItem, as retrieved by [getValue()](FormItem.md#method-formitemgetvalue) and set via [setValue()](FormItem.md#method-formitemsetvalue), is an Array of Strings reflecting the selected values.

When this value is true, we disable doubleClick events by default, instead issuing two single clicks by forcibly setting [noDoubleClicks: true](Canvas.md#attr-canvasnodoubleclicks). If you need to work with doubleClick events, you can disable this default behavior by explicitly setting formItem.pickListProperties.noDoubleClicks: false.

Note: `multiple:true` SelectItems with multipleAppearance:"grid" do not currently support optionDataSource binding. You can get around this by calling [DataSource.fetchData](DataSource.md#method-datasourcefetchdata) directly and calling [dsResponse.data.getValueMap()](List.md#method-listgetvaluemap) to obtain a valueMap.

If the `multiple` attribute is not explicitly specified, it will default to `false`, unless thie item has a specified [valueMap](FormItem.md#attr-formitemvaluemap) and is part of a [filter interface](SearchForm.md#class-searchform) with [SearchForm.useMultiSelectForValueMaps](SearchForm.md#attr-searchformusemultiselectforvaluemaps) set to true.

### Groups

- formValues
- appearance

**Flags**: IRW

---
## Method: SelectItem.defaultDynamicValue

### Description
Expression evaluated to determine the [SelectItem.defaultValue](#attr-selectitemdefaultvalue) when no value is provided for this item. To default to the first option use [SelectItem.defaultToFirstOption](#attr-selectitemdefaulttofirstoption) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| values | [Object](../main.md#type-object) | false | — | the current set of values for the form as a whole |

### Returns

`[Any](#type-any)` — dynamically calculated default value for this item

**Flags**: A

---
## Method: SelectItem.getValueFieldName

### Description
Getter method to retrieve the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item. For items with a specified [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this determines which field in that dataSource corresponds to the value for this item.

If unset, if a [foreignKey relationship](DataSourceField.md#attr-datasourcefieldforeignkey) exists between this field and the optionDataSource, this will be used, otherwise default behavior will return the [FormItem.name](FormItem.md#attr-formitemname) of this field.

### Returns

`[String](#type-string)` — fieldName to use a "value field" in records from this items [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource)

### Groups

- display_values

**Flags**: A

---
## Method: SelectItem.getSelectedRecords

### Description
For a SelectItem with an [SelectItem.optionDataSource](#attr-selectitemoptiondatasource) and allowing multiple selection ([via multiple:true](#attr-selectitemmultiple)), returns the list of currently selected records, or null if none are selected.

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — the list of selected records, or null if none are selected

---
## Method: SelectItem.dataArrived

### Description
If this item is showing a dataBound pickList, this notification method will be fired when new data arrives from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../main.md#type-int) | false | — | index of first row returned by the server |
| endRow | [int](../main.md#type-int) | false | — | index of last row returned by the server |
| data | [ResultSet](#type-resultset) | false | — | pointer to this pickList's data |

---
## Method: SelectItem.fetchData

### Description
Only applies to databound items (see [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)).  
Performs a fetch type operation on this item's DataSource to retrieve the set of valid options for the item, based on the current [PickList.pickListCriteria](PickList.md#attr-picklistpicklistcriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../main_2.md#type-dscallback) | true | — | Callback to fire when the fetch completes. Callback will fire with 4 parameters:

*   `item` a pointer to the form item
*   `dsResponse` the [DSResponse](DSResponse.md#class-dsresponse) returned by the server
*   `data` the raw data returned by the server
*   `dsRequest` the [DSRequest](../main_2.md#object-dsrequest) sent to the server |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | properties to apply to the dsRequest for this fetch. |

---
## Method: SelectItem.setValue

### Description
Set the value of the form item to the value passed in

NOTE: for valueMap'd items, newValue should be data value not displayed value

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Any](#type-any) | false | — | value to set the element to |

---
## Method: SelectItem.getDisplayFieldName

### Description
Returns the `displayField` for this item.

Behavior varies based on the configuration of this item, as follows:

*   If this item has an [SelectItem.optionDataSource](#attr-selectitemoptiondatasource) and an explicit [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) is specified, this will be returned.
*   Otherwise if an explicit [SelectItem.displayField](#attr-selectitemdisplayfield) is specified it will be returned by default. If the `displayField` was specified on the underlying dataSource field, and no matching field is present in the [SelectItem.optionDataSource](#attr-selectitemoptiondatasource) for the item, we avoid returning the specified displayField value and instead return the title field of the option DataSource. We do this to avoid confusion for the case where the displayField is intended as a display-field value for showing another field value within the same record in the underlying dataSource only.
*   If no explicit foreignDisplay or displayField specification was found, and the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item is hidden in the [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this method will return the title field for the `optionDataSource`.

### Returns

`[FieldName](../main.md#type-fieldname)` — display field name, or null if there is no separate display field to use.

**Flags**: A

---
## Method: SelectItem.showPicker

### Description
Method to show a picker for this item. By default this method is called if the user clicks on a [pickerIcon](#attr-selectitemshowpickericon). May also be called programmatically.

Overridden from the default [FormItem.showPicker](FormItem.md#method-formitemshowpicker) implementation to show the [PickList](../main_2.md#interface-picklist)

---
## Method: SelectItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this `SelectItem` should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, a [multiple](#attr-selectitemmultiple) `SelectItem` when displayed in the pending state will apply [FormItem.editPendingCSSText](FormItem.md#attr-formitemeditpendingcsstext) to any new value in the text box and also append "Pending" to the cells' [ListGrid.baseStyle](ListGrid_1.md#attr-listgridbasestyle) for cells in the pickList menu corresponding to new values. Returning `false` will cancel this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing `DynamicForm` instance. |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this"). |
| pendingStatus | [boolean](../main.md#type-boolean) | false | — | `true` if the item should show its pending visual state; `false` otherwise. |
| newValue | [Any](#type-any) | false | — | the current form item value. |
| value | [Any](#type-any) | false | — | the value that would be restored by a call to [DynamicForm.resetValues](DynamicForm.md#method-dynamicformresetvalues). |

### Returns

`[boolean](../main.md#type-boolean)` — `false` to cancel the default behavior.

---
## Method: SelectItem.setValueMap

### Description
Set the valueMap for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valueMap | [Array](#type-array)|[Object](../main.md#type-object) | false | — | new valueMap |

### Groups

- valueMap

### See Also

- [FormItem.valueMap](FormItem.md#attr-formitemvaluemap)

---
## Method: SelectItem.getSelectedRecord

### Description
Get the record returned from the [SelectItem.optionDataSource](#attr-selectitemoptiondatasource) when [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) is true, and the missing value is fetched.

[FormItem.fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) kicks off the fetch when the form item is initialized with a non null value or when setValue() is called on the item. Note that this method will return null before the fetch completes, or if no record is found in the optionDataSource matching the underlying value.

### Returns

`[ListGridRecord](#type-listgridrecord)` — selected record

### Groups

- display_values

---
