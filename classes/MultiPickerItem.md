# MultiPickerItem Documentation

[← Back to API Index](../main.md)

---

## Class: MultiPickerItem

*Inherits from:* [StaticTextItem](StaticTextItem.md#class-statictextitem)

### Description
MultiPickerItem provides an interface to edit data involving whether a record has membership in a certain set, for example, where specific Employees are part of specific Teams.

MultiPickerItem is a compact editor for this purpose, using a [pop-up](#attr-multipickeritempickerlayout) to present a [Shuttle](Shuttle.md#class-shuttle)-style interface for moving records or values being different categories. When the MultiPickerItem pop-up is not active, MultiPickerItem just displays the currently chosen values as read-only text, which can be [clipped](StaticTextItem.md#attr-statictextitemclipvalue) to appear in a very small space.

**Note**: if your use case is a _search_ interface to generate criteria, in either the FilterEditor of a ListGrid/TreeGrid, or in a SearchForm, SetFilterItem is the right choice. Generally, use SetFilterItem for searching, and MultiPickerItem (or [Shuttle](Shuttle.md#class-shuttle)) for editing.

To configure a MultiPickerItem, provide either an optionDataSource or a valueMap. The [value](FormItem.md#method-formitemgetvalue) stored by a MultiPickerItem is the set of selected items, as either a list of [primary key values](DataSourceField.md#attr-datasourcefieldprimarykey) if an optionDataSource is used, or as just ID values if an valueMap is used.

The item's picker-component can be customized via settings such as [sortField](#attr-multipickeritemsortfield), or by configuring [auto-children](../main.md#type-autochild) like the [search-form](#attr-multipickeritemfilterform), the [main pickList-grid](#attr-multipickeritempicklist) or the separate list of [selected values](#attr-multipickeritemselectionlist). You can use [MultiPickerItem.optionFilterContext](#attr-multipickeritemoptionfiltercontext) to apply custom `requestProperties` to fetches from the main `pickList` grid.

---
## Attr: MultiPickerItem.canSelectFolders

### Description
For multiPickerItems with [selectionStyle:"pickTree"](../main.md#type-selectionstyle), should the user be able to select and deselect folders?

If false, selection checkboxes will only be visible by leaf nodes within the pickTree data set.

Note that this flag may be set to true in conjunction with [includeSelectedParents:false](#attr-multipickeritemincludeselectedparents). In this case the user may check and uncheck parent nodes as a convenient way to select or unselect all their children due to [cascading selection](#attr-multipickeritemcascadeselection), but the parent nodes themselves won't be present in the item's value.

**Flags**: IR

---
## Attr: MultiPickerItem.textMatchStyle

### Description
textMatchStyle to apply to [option criteria](#method-multipickeritemgetoptioncriteria) for this item

**Flags**: IR

---
## Attr: MultiPickerItem.cascadeSelection

### Description
For multiPickerItems with [selectionStyle:"pickTree"](../main.md#type-selectionstyle), and [canSelectFolders:true](#attr-multipickeritemcanselectfolders), should [TreeGrid.cascadeSelection](TreeGrid.md#attr-treegridcascadeselection) be enabled on our pickTree?

**Flags**: IR

---
## Attr: MultiPickerItem.pickList

### Description
The MultiPickerItem `pickList` is a filterable ListGrid [AutoChild](../main.md#type-autochild) for viewing and selecting the list of available options when [SelectionStyle](../main.md#type-selectionstyle) is `"pickList"`.

It is rendered inside the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) along with the optional [MultiPickerItem.selectionList](#attr-multipickeritemselectionlist)

**Flags**: IR

---
## Attr: MultiPickerItem.showSelectionList

### Description
Should a [list of selected items](#attr-multipickeritemselectionlist) be displayed below the [PickList](../main_2.md#interface-picklist) if [SelectionStyle](../main.md#type-selectionstyle) is `"pickList"`?

**Flags**: IR

---
## Attr: MultiPickerItem.expansionWidth

### Description
Width for the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) in expanded mode when [MultiPickerItem.canExpand](#attr-multipickeritemcanexpand) is true

**Flags**: IRW

---
## Attr: MultiPickerItem.shuttleHeight

### Description
Height for the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) when [SelectionStyle](../main.md#type-selectionstyle) is `"shuttle"`.

**Flags**: IRW

---
## Attr: MultiPickerItem.filterIconSrc

### Description
[src](FormItemIcon.md#attr-formitemiconsrc) for the [MultiPickerItem.filterIcon](#attr-multipickeritemfiltericon)

**Flags**: IR

---
## Attr: MultiPickerItem.selectionListLabel

### Description
AutoChild to show the [MultiPickerItem.selectedSelectionListTitle](#attr-multipickeritemselectedselectionlisttitle)

**Flags**: IR

---
## Attr: MultiPickerItem.pickerLayout

### Description
Main dropdown picker layout containing the [PickList](../main_2.md#interface-picklist) or [Shuttle](Shuttle.md#class-shuttle).

**Flags**: IR

---
## Attr: MultiPickerItem.optionDataSource

### Description
If set, this FormItem will map stored values to display values as though a [ValueMap](../main_2.md#type-valuemap) were specified, by fetching records from the specified `optionDataSource` and extracting the [valueField](FormItem.md#attr-formitemvaluefield) and [displayField](FormItem.md#attr-formitemdisplayfield) in loaded records, to derive one valueMap entry per record loaded from the optionDataSource.

With the default setting of [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues), fetches will be initiated against the optionDataSource any time the FormItem has a non-null value and no corresponding display value is available. This includes when the form is first initialized, as well as any subsequent calls to [FormItem.setValue](FormItem.md#method-formitemsetvalue), such as may happen when [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) is called. Retrieved values are automatically cached by the FormItem.

Note that if a normal, static [valueMap](FormItem.md#attr-formitemvaluemap) is **also** specified for the field (either directly in the form item or as part of the field definition in the dataSource), it will be preferred to the data derived from the optionDataSource for whatever mappings are present.

In a databound form, if [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) is specified for a FormItem and `optionDataSource` is unset, `optionDataSource` will default to the form's current DataSource

### Groups

- display_values

### See Also

- [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

**Flags**: IR

---
## Attr: MultiPickerItem.selectAllButtonTitle

### Description
Title for the [MultiPickerItem.selectAllButton](#attr-multipickeritemselectallbutton)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiPickerItem.sortDirection

### Description
[Sort direction](ListGrid_1.md#attr-listgridsortdirection) for this item's list of options. Will be applied to the +link{MultiPickeπrItem.pickList}, [MultiPickerItem.pickTree](#attr-multipickeritempicktree) or [MultiPickerItem.shuttle](#attr-multipickeritemshuttle) depending on the [MultiPickerItem.selectionStyle](#attr-multipickeritemselectionstyle) of this item.

**Flags**: IR

---
## Attr: MultiPickerItem.pickListWidth

### Description
Default width for the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) when [SelectionStyle](../main.md#type-selectionstyle) is `"pickList"`.

**Flags**: IRW

---
## Attr: MultiPickerItem.selectAllButton

### Description
Select All button [AutoChild](../main.md#type-autochild)

**Flags**: IR

---
## Attr: MultiPickerItem.filterHint

### Description
[Hint](FormItem.md#attr-formitemhint) for the [MultiPickerItem.filterForm](#attr-multipickeritemfilterform) text item.

This will be shown inside the field via [TextItem.showHintInField](TextItem.md#attr-textitemshowhintinfield)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiPickerItem.expandIconSrc

### Description
[SCImgURL](../main.md#type-scimgurl) for the [MultiPickerItem.expansionIcon](#attr-multipickeritemexpansionicon) while not in expanded mode

**Flags**: IR

---
## Attr: MultiPickerItem.filterIconWidth

### Description
[width](FormItemIcon.md#attr-formitemiconwidth) for the [MultiPickerItem.filterIcon](#attr-multipickeritemfiltericon)

**Flags**: IR

---
## Attr: MultiPickerItem.deselectAllWhileFiltered_partialCachePrompt

### Description
Disabled prompt for the [MultiPickerItem.deselectAllButton](#attr-multipickeritemdeselectallbutton) while filtered if [MultiPickerItem.selectAllWhileFiltered](#attr-multipickeritemselectallwhilefiltered) is set to `"whenLoaded"` and the [PickList](../main_2.md#interface-picklist) does not have a complete data set loaded on the client.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: MultiPickerItem.includeSelectedParents

### Description
For multiPickerItems with [selectionStyle:"pickTree"](../main.md#type-selectionstyle), and [canSelectFolders:true](#attr-multipickeritemcanselectfolders), should selected parent nodes be included in the item's value?

When [cascading selection](#attr-multipickeritemcascadeselection) is enabled for a tree, the selected state of parent nodes always reflects the selected state of their children, and it may not be necessary or desirable to explicitly record the parents' selected state in the item's value.

Some specific use cases where this is the case might include:

*   Creating filter criteria for a target TreeGrid where [TreeGrid.keepParentsOnFilter](TreeGrid.md#attr-treegridkeepparentsonfilter) is true. In this case filter criteria would not need to include selected parent nodes for the children to be visible in the target tree.
*   Trees where leaves are of a different logical type than their parents. If a tree structure is being used to categorize data, [cascading selection](#attr-multipickeritemcascadeselection) may be useful to allow the user to easily select all items within a category but application code may not want to include the categories as part of a MultiPickerItem's value

This property only applies when [MultiPickerItem.cascadeSelection](#attr-multipickeritemcascadeselection) is true. If cascadeSelection is false, all selected nodes will be present in the items value regardless of their parent/child relationships.

**Flags**: IR

---
## Attr: MultiPickerItem.displayField

### Description
If set, this item will display a value from another field to the user instead of showing the underlying data value for the [field name](FormItem.md#attr-formitemname).

This property is used in two ways:

The item will display the displayField value from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues) if [FormItem.useLocalDisplayFieldValue](FormItem.md#attr-formitemuselocaldisplayfieldvalue) is true, (or if unset and the conditions outlined in the documentation for that property are met).

If this field has an [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property is used by default to identify which value to use as a display value in records from this related dataSource. In this usage the specified displayField must be explicitly defined in the optionDataSource to be used - see [getDisplayFieldName()](FormItem.md#method-formitemgetdisplayfieldname) for more on this behavior.  
If not using [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue), the display value for this item will be derived by performing a fetch against the [option dataSource](FormItem.md#method-formitemgetoptiondatasource) to find a record where the [value field](FormItem.md#method-formitemgetvaluefieldname) matches this item's value, and use the `displayField` value from that record.  
In addition to this, PickList-based form items that provide a list of possible options such as the [SelectItem](SelectItem.md#class-selectitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) will show the `displayField` values to the user by default, allowing them to choose a new data value (see [FormItem.valueField](FormItem.md#attr-formitemvaluefield)) from a list of user-friendly display values.

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

**Flags**: IR

---
## Attr: MultiPickerItem.selectedSelectionListTitle

### Description
Default title for the [MultiPickerItem.selectionList](#attr-multipickeritemselectionlist).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiPickerItem.expansionIcon

### Description
Automatically generated expand / collapse icon when [MultiPickerItem.canExpand](#attr-multipickeritemcanexpand) is true

**Flags**: IR

---
## Attr: MultiPickerItem.multiple

### Description
MultiPickerItems always work with array values

**Flags**: IR

---
## Attr: MultiPickerItem.filterPickListOnKeypress

### Description
Should [filterOnKeypress](ListGrid_1.md#attr-listgridfilteronkeypress) be active for the pickList?

This behavior applies to filter values entered in the [MultiPickerItem.filterForm](#attr-multipickeritemfilterform) as well as the the standard filterEditor for the picklist in [expanded view](#attr-multipickeritemcanexpand).

**Flags**: IR

---
## Attr: MultiPickerItem.deselectAllWhileFiltered_disabledPrompt

### Description
Disabled prompt for the [MultiPickerItem.deselectAllButton](#attr-multipickeritemdeselectallbutton) while filtered if [MultiPickerItem.selectAllWhileFiltered](#attr-multipickeritemselectallwhilefiltered) is set to `"disable"`.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: MultiPickerItem.optionOperationId

### Description
If this item has a specified `optionDataSource`, this attribute may be set to specify an explicit [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) when performing a fetch against the option dataSource to pick up display value mapping.

### Groups

- databinding

**Flags**: IR

---
## Attr: MultiPickerItem.deriveUniqueValues

### Description
If this MultiPickerItem is deriving its options from a dataSource, should it ensure unique field values by [grouping by](DSRequest.md#attr-dsrequestgroupby) the value field for this item? This is not necessary if the target dataSource value field is already unique - for example if this is the primaryKey field for a dataSource.

Note that for MultiPickerItems with `deriveUniqueValues:true`, any [MultiPickerItem.expandedPickListFields](#attr-multipickeritemexpandedpicklistfields) to be displayed in the [expanded view](#attr-multipickeritemcanexpand) will not be able to display meaningful values unless a [summaryFunction](DSRequest.md#attr-dsrequestsummaryfunctions) is supplied to produce aggregated values from the grouped data. This may be achieved by specifying summaryFunctions directly on the [MultiPickerItem.optionFilterContext](#attr-multipickeritemoptionfiltercontext), or on the [operationBinding](DataSource.md#attr-datasourceoperationbindings) for the [fetch operation](#attr-multipickeritemoptionoperationid).

**Flags**: IRA

---
## Attr: MultiPickerItem.showSelectionLabel

### Description
Should we show a [MultiPickerItem.selectionListLabel](#attr-multipickeritemselectionlistlabel) for the [MultiPickerItem.selectedSelectionListTitle](#attr-multipickeritemselectedselectionlisttitle) above the [MultiPickerItem.selectionList](#attr-multipickeritemselectionlist).

Will never be shown if [MultiPickerItem.showSelectionList](#attr-multipickeritemshowselectionlist) is false or if selectionStyle is not "pickList".

**Flags**: IR

---
## Attr: MultiPickerItem.pickListFetchDelay

### Description
If [MultiPickerItem.filterPickListOnKeypress](#attr-multipickeritemfilterpicklistonkeypress) is true, how long to wait in ms after the last keystroke from a user before filtering the pickList.

If not explicitly specified, the default fetchDelay will be derived from [the pickList fetchDelay](ListGrid_1.md#attr-listgridfetchdelay).

**Flags**: IR

---
## Attr: MultiPickerItem.canExpand

### Description
Should we show an [MultiPickerItem.expansionIcon](#attr-multipickeritemexpansionicon) expand button allowing the user to show an expanded view of the [MultiPickerItem.pickList](#attr-multipickeritempicklist) with multiple fields.

`canExpand` only applies to MultiPickerItems with selectionStyle set to "pickList" or "pickTree" and an explicitly specified set of [MultiPickerItem.expandedPickListFields](#attr-multipickeritemexpandedpicklistfields) to display within the expanded view.

**Flags**: IR

---
## Attr: MultiPickerItem.shuttleWidth

### Description
Width for the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) when [SelectionStyle](../main.md#type-selectionstyle) is `"shuttle"`.

**Flags**: IRW

---
## Attr: MultiPickerItem.initialSort

### Description
[Initial sort specifiers](ListGrid_1.md#attr-listgridinitialsort) for this item's list of options. Will be applied to the [MultiPickerItem.pickList](#attr-multipickeritempicklist), [MultiPickerItem.pickTree](#attr-multipickeritempicktree) or [MultiPickerItem.shuttle](#attr-multipickeritemshuttle) depending on the [MultiPickerItem.selectionStyle](#attr-multipickeritemselectionstyle) of this item.

**Flags**: IR

---
## Attr: MultiPickerItem.expandedPickListFields

### Description
If [MultiPickerItem.canExpand](#attr-multipickeritemcanexpand) is true, this is the list of fields to display in the [PickList](../main_2.md#interface-picklist) or [MultiPickerItem.pickTree](#attr-multipickeritempicktree) when the picker is expanded

**Flags**: IR

---
## Attr: MultiPickerItem.selectionList

### Description
Automatically generated ListGrid displaying the current selection for [selectionStyle:"pickList"](../main.md#type-selectionstyle).

Has [canRemoveRecords](ListGrid_1.md#attr-listgridcanremoverecords) enabled as an alternative UI for deselecting records to unchecking the item in the [PickList](../main_2.md#interface-picklist).

**Flags**: IR

---
## Attr: MultiPickerItem.selectAllWhileFiltered_partialCachePrompt

### Description
Disabled prompt for the [MultiPickerItem.selectAllButton](#attr-multipickeritemselectallbutton) while filtered if [MultiPickerItem.selectAllWhileFiltered](#attr-multipickeritemselectallwhilefiltered) is set to `"whenLoaded"` and the [PickList](../main_2.md#interface-picklist) does not have a complete data set loaded on the client.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: MultiPickerItem.deselectAllButtonTitle

### Description
Title for the [MultiPickerItem.deselectAllButton](#attr-multipickeritemdeselectallbutton)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiPickerItem.showFilterForm

### Description
Should the [MultiPickerItem.filterForm](#attr-multipickeritemfilterform) be shown?

This only applies to selectionStyle "pickList".

**Flags**: IR

---
## Attr: MultiPickerItem.collapseIconSrc

### Description
[SCImgURL](../main.md#type-scimgurl) for the [MultiPickerItem.expansionIcon](#attr-multipickeritemexpansionicon) while in expanded mode

**Flags**: IR

---
## Attr: MultiPickerItem.pickListFields

### Description
Optional list of fields for the [MultiPickerItem.pickList](#attr-multipickeritempicklist). This property may be used to customize the appearance of the field / fields in the pickList.

If not explicitly specified, pick list fields will be generated automatically to show the display field (or value field if there is no display field) for each option.

Note that if [MultiPickerItem.canExpand](#attr-multipickeritemcanexpand) is true, developers should use [MultiPickerItem.expandedPickListFields](#attr-multipickeritemexpandedpicklistfields) to specify the set of fields to display in the expanded view.

**Flags**: IR

---
## Attr: MultiPickerItem.sortField

### Description
[Sort field](ListGrid_1.md#attr-listgridsortfield) for this item's list of options. Will be applied to the [MultiPickerItem.pickList](#attr-multipickeritempicklist), [MultiPickerItem.pickTree](#attr-multipickeritempicktree) or [MultiPickerItem.shuttle](#attr-multipickeritemshuttle) depending on the [MultiPickerItem.selectionStyle](#attr-multipickeritemselectionstyle) of this item.

**Flags**: IR

---
## Attr: MultiPickerItem.pickerToolbar

### Description
Toolbar autoChild containing the [MultiPickerItem.selectAllButton](#attr-multipickeritemselectallbutton), [MultiPickerItem.deselectAllButton](#attr-multipickeritemdeselectallbutton) and [MultiPickerItem.expansionIcon](#attr-multipickeritemexpansionicon).

Shown within the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) if [SelectionStyle](../main.md#type-selectionstyle) is `"pickList"`

**Flags**: IR

---
## Attr: MultiPickerItem.optionFilterContext

### Description
If this item has a specified `optionDataSource`, and this property is not null, the context is passed to the dataSource as [RPCRequest](../main.md#object-rpcrequest) properties when performing fetch operations on the dataSource to obtain a data-value to display-value mapping, and when fetching for grid-based pickers.

This attribute is a direct shortcut for setting fetch-request properties via `item.pickerProperties.dataProperties.requestProperties`.

**Flags**: IR

---
## Attr: MultiPickerItem.filterIconHeight

### Description
[height](FormItemIcon.md#attr-formitemiconheight) for the [MultiPickerItem.filterIcon](#attr-multipickeritemfiltericon)

**Flags**: IR

---
## Attr: MultiPickerItem.selectionStyle

### Description
Should the MultiPickerItem use a [Shuttle](Shuttle.md#class-shuttle) style interface to indicate the currently selected / unselected values?

**Flags**: IRA

---
## Attr: MultiPickerItem.valueField

### Description
If this form item maps data values to display values by retrieving the [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) values from an [optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property denotes the the field to use as the underlying data value in records from the optionDataSource.  
If not explicitly supplied, the valueField name will be derived as described in [FormItem.getValueFieldName](FormItem.md#method-formitemgetvaluefieldname).

### Groups

- databinding

**Flags**: IR

---
## Attr: MultiPickerItem.shuttle

### Description
AutoChild [Shuttle](Shuttle.md#class-shuttle) shown in the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) when [SelectionStyle](../main.md#type-selectionstyle) is set to `"shuttle"`.

**Flags**: IR

---
## Attr: MultiPickerItem.optionCriteria

### Description
If this MultiPickerItem is deriving its options from a dataSource, this property allows developers to specify criteria for the fetch.

**Flags**: IRWA

---
## Attr: MultiPickerItem.selectAllWhileFiltered

### Description
If the user has filtered the set of options available in this item, how should the "Select All" and "Clear All" buttons work?

**Flags**: IRA

---
## Attr: MultiPickerItem.pickTree

### Description
The MultiPickerItem `pickTree` is a TreeGrid [AutoChild](../main.md#type-autochild) for viewing and selecting a tree of available options when [SelectionStyle](../main.md#type-selectionstyle) is `"pickTree"`.

It is rendered inside the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) along with the optional [MultiPickerItem.selectionList](#attr-multipickeritemselectionlist)

**Flags**: IR

---
## Attr: MultiPickerItem.filterIcon

### Description
Automatically generated right-aligned inline filter indicator icon for the [MultiPickerItem.filterForm](#attr-multipickeritemfilterform) text box.

This icon may be customized using the standard AutoChild pattern as well as via [MultiPickerItem.filterIconSrc](#attr-multipickeritemfiltericonsrc), [MultiPickerItem.filterIconWidth](#attr-multipickeritemfiltericonwidth), [MultiPickerItem.filterIconHeight](#attr-multipickeritemfiltericonheight)

**Flags**: IR

---
## Attr: MultiPickerItem.pickListHeight

### Description
Default height for the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) when [SelectionStyle](../main.md#type-selectionstyle) is `"pickList"`.

**Flags**: IRW

---
## Attr: MultiPickerItem.deselectAllButton

### Description
Clear All button [AutoChild](../main.md#type-autochild)

**Flags**: IR

---
## Attr: MultiPickerItem.expansionHeight

### Description
Height for the [MultiPickerItem.pickerLayout](#attr-multipickeritempickerlayout) in expanded mode when [MultiPickerItem.canExpand](#attr-multipickeritemcanexpand) is true

**Flags**: IRW

---
## Attr: MultiPickerItem.selectAllWhileFiltered_disabledPrompt

### Description
Disabled prompt for the [MultiPickerItem.selectAllButton](#attr-multipickeritemselectallbutton) while filtered if [MultiPickerItem.selectAllWhileFiltered](#attr-multipickeritemselectallwhilefiltered) is set to `"disable"`.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: MultiPickerItem.filterForm

### Description
Dynamic form showing a single text item for filtering the [PickList](../main_2.md#interface-picklist) while [SelectionStyle](../main.md#type-selectionstyle) is "pickList".

May be hidden by setting [MultiPickerItem.showFilterForm](#attr-multipickeritemshowfilterform) to false.

If [MultiPickerItem.canExpand](#attr-multipickeritemcanexpand) is true, the filter form will not be displayed in the expanded view, as it would be unclear to the user which of the expanded fields would be filtered by it.

Instead if `showFilterForm` is true, the pickList will show the [filterEditor](ListGrid_1.md#attr-listgridfiltereditor) by default, allowing the user to filter by [field](#attr-multipickeritemexpandedpicklistfields)

Instead of the filterForm, developers may display the standard filterEditor for the pickList in non-expanded view via [pickList autoChild properties](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren). If you do this the filterForm will not be displayed even if`showFilterForm` is true.

**Flags**: IR

---
## Method: MultiPickerItem.getOptionCriteria

### Description
Return the derived [MultiPickerItem.optionCriteria](#attr-multipickeritemoptioncriteria) for this item

### Returns

`[Criteria](../main_2.md#type-criteria)` — criteria to apply to the pickList and expandedPickerGrid

---
## Method: MultiPickerItem.getValueFieldName

### Description
Getter method to retrieve the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item. For items with a specified [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this determines which field in that dataSource corresponds to the value for this item.

If unset, if a [foreignKey relationship](DataSourceField.md#attr-datasourcefieldforeignkey) exists between this field and the optionDataSource, this will be used, otherwise default behavior will return the [FormItem.name](FormItem.md#attr-formitemname) of this field.

### Returns

`[String](#type-string)` — fieldName to use a "value field" in records from this items [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource)

### Groups

- display_values

---
