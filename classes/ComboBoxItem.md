# ComboBoxItem Documentation

[← Back to API Index](../reference.md)

---

## Class: ComboBoxItem

*Inherits from:* [TextItem](TextItem.md#class-textitem)

### Description
The Combobox is a text input field which can show a list of options via a drop-down PickList.

The set of options will be filtered based on the current value in the text field, so only options that match what has been typed so far will be displayed. The set of options can be derived from a ValueMap or dynamically retrieved from a dataSource. See the [PickList](../reference_2.md#interface-picklist) interface for further settings.

The two most common use cases for ComboBoxItems are:

*   With [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) set to true, the ComboBoxItem acts as a freeform text entry field with the picklist providing essentially a set of suggested completions similar to a URL bar in a web browser.
*   With [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) set to false, the ComboBoxItem acts similarly to a SelectItem where a fixed set of options is available to the user and the text entry field is essentially used to filter which of these options are visible

Other commonly used settings to configure ComboBoxItem behavior are:  
\- [ComboBoxItem.defaultToFirstOption](#attr-comboboxitemdefaulttofirstoption) - this will select the first option from the pickList as a default value for the item - and  
\- [ComboBoxItem.completeOnTab](#attr-comboboxitemcompleteontab) which causes the current selection in the pickList (if there is one) to be chosen when the user tabs out of the field, allowing a user to type a few characters and hit tab to auto-complete to the first matched option. `completeOnTab` is automatically set to true if [addUnknownValues](#attr-comboboxitemaddunknownvalues) is false.

ComboBoxItem does not provide built-in support for multiple selection. For a Combobox that does provide such a multiple-select feature use [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem).

### See Also

- [PickList](../reference_2.md#interface-picklist)

---
## Attr: ComboBoxItem.pickerExitButton

### Description
[NavigationButton](NavigationButton.md#class-navigationbutton) to dismiss the picker interface, created when [ComboBoxItem.pickListPlacement](#attr-comboboxitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pickerExitButtonTitle](#attr-comboboxitempickerexitbuttontitle) for [Button.title](Button.md#attr-buttontitle)

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.pendingTextBoxStyle

### Description
Optional "pending" style for this item's text box.

If [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) is false, when the user modifies the value displayed in the combobox item text box, the underlying data value (as returned from item.getValue()) is not immediately updated - instead the value is used to filter the set of results displayed in the comboBoxItem pickList.

While the comboBoxItem is in this pending state (where the result of getEnteredValue() will not necessarily match the display value for whatever is returned by getValue()), the pendingTextBoxStyle may be applied to the text box for the item.

When the element value is updated to display the actual value for the item (typically due to the user selecting a value from the pickList), the standard [TextItem.textBoxStyle](TextItem.md#attr-textitemtextboxstyle) will be reapplied.

May be left unset in which case the standard text box style is always applied. Has no effect if [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) is true.

**Flags**: IRW

---
## Attr: ComboBoxItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ComboBoxItem.completeOnEnter

### Description
If true, when the pickList is showing, the user can select the current value by hitting the `Enter` key.

If not explicitly set, completeOnEnter will default to false for items embedded in a [filtering interface](SearchForm.md#class-searchform), true otherwise.

**Flags**: IRW

---
## Attr: ComboBoxItem.sortField

### Description
Specifies one or more fields by which this item should be initially sorted. It can be a [field name](ListGridField.md#attr-listgridfieldname), or an array of field names - but note that, if multiple fields are supplied, then each will be sorted in the same [direction](ListGrid_1.md#attr-listgridsortdirection).

For full sorting control, set [initialSort](PickList.md#attr-picklistinitialsort) to a list of custom [sortSpecifiers](../reference.md#object-sortspecifier).

This attribute can also be set to the index of a field in the fields array, but note that it will be converted to a string (field name) after initialization.

### Groups

- sorting

**Flags**: IR

---
## Attr: ComboBoxItem.separateValuesList

### Description
AutoChild used to show [ComboBoxItem.specialValues](#attr-comboboxitemspecialvalues).

**Flags**: IR

---
## Attr: ComboBoxItem.filterLocally

### Description
If `filterLocally` is set for this item, and this item is showing options from a dataSource, fetch the entire set of options from the server, and use these values to map the item value to the appropriate display value. Also use `"local"` type filtering on drop down list of options.

This means data will only be fetched once from the server, and then filtered on the client.

Note - when this property is set to `false`, filtering will still be performed on the client if a complete set of data for some criteria has been cached by a fetch, and a subsequent fetch has more restrictive criteria. To explicitly disable client-side filtering set the [ComboBoxItem.useClientFiltering](#attr-comboboxitemuseclientfiltering) property to false.

### See Also

- [FormItem.filterLocally](FormItem.md#attr-formitemfilterlocally)

**Flags**: IRA

---
## Attr: ComboBoxItem.useClientFiltering

### Description
For [databound](#attr-comboboxitemoptiondatasource) items, this property will be passed to the generated ResultSet data object for the pickList as [ResultSet.useClientFiltering](ResultSet.md#attr-resultsetuseclientfiltering). Setting to false will disable filtering on the client and ensure criteria are always passed to the DataSource directly.

**Flags**: IRA

---
## Attr: ComboBoxItem.pickListCriteria

### Description
If this item has a databound pickList (for example [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource) is set), this property can be used to provide static filter criteria when retrieving the data for the pickList.

### Groups

- pickList

**Flags**: IRWA

---
## Attr: ComboBoxItem.displayField

### Description
If set, this item will display a value from another field to the user instead of showing the underlying data value for the [field name](FormItem.md#attr-formitemname).

This property is used in two ways:

The item will display the displayField value from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues) if [FormItem.useLocalDisplayFieldValue](FormItem.md#attr-formitemuselocaldisplayfieldvalue) is true, (or if unset and the conditions outlined in the documentation for that property are met).

If this field has an [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property is used by default to identify which value to use as a display value in records from this related dataSource. In this usage the specified displayField must be explicitly defined in the optionDataSource to be used - see [ComboBoxItem.getDisplayFieldName](#method-comboboxitemgetdisplayfieldname) for more on this behavior.  
If not using [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue), the display value for this item will be derived by performing a fetch against the [option dataSource](FormItem.md#method-formitemgetoptiondatasource) to find a record where the [value field](FormItem.md#method-formitemgetvaluefieldname) matches this item's value, and use the `displayField` value from that record.  
In addition to this, PickList-based form items that provide a list of possible options such as the [SelectItem](SelectItem.md#class-selectitem) or [ComboBoxItem](#class-comboboxitem) will show the `displayField` values to the user by default, allowing them to choose a new data value (see [FormItem.valueField](FormItem.md#attr-formitemvaluefield)) from a list of user-friendly display values.

This essentially allows the specified `optionDataSource` to be used as a server based [valueMap](../reference.md#kb-topic-valuemap).

If [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, selecting a new value will update both the value for this field and the associated display-field value on the record being edited.

Note: Developers may specify the [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) property in addition to `displayField`. This is useful for cases where the display field name in the local dataSource differs from the display field name in the optionDataSource. See the documentation for [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) for more on this.  
If a foreignDisplayField is specified, as with just displayField, if [local display values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](FormItem.md#attr-formitemstoredisplayvalues) is true, when the user chooses a value the associated display-field value on the record being edited will be updated. In this case it would be set to the foreignDisplayField value from the related record. This means foreignDisplayField is always expected to be set to the equivalent field in the related dataSources.  
Developers looking to display some _other_ arbitrary field(s) from the related dataSource during editing should consider using custom [PickList.pickListFields](PickList.md#attr-picklistpicklistfields) instead of setting a foreignDisplayField.

Note that if `optionDataSource` is set and no valid display field is specified, [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname) will return the dataSource title field by default.

If a displayField is specified for a freeform text based item (such as a [ComboBoxItem](#class-comboboxitem)), any user-entered value will be treated as a display value. In this scenario, items will derive the data value for the item from the first record where the displayField value matches the user-entered value. To avoid ambiguity, developers may wish to avoid this usage if display values are not unique.

### Groups

- databinding

### See Also

- [FormItem.getDisplayFieldName](FormItem.md#method-formitemgetdisplayfieldname)
- [FormItem.invalidateDisplayValueCache](FormItem.md#method-formiteminvalidatedisplayvaluecache)

**Flags**: IRW

---
## Attr: ComboBoxItem.pickerExitButtonTitle

### Description
The title for the [ComboBoxItem.pickerExitButton](#attr-comboboxitempickerexitbutton).

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.emptyPickListMessage

### Description
Empty message to display in the comboboxItem if [PickList.hideEmptyPickList](PickList.md#attr-picklisthideemptypicklist) is `false`.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: ComboBoxItem.searchStringTooShortMessage

### Description
Message to display in pick list when [minimumSearchLength](#attr-comboboxitemminimumsearchlength) characters have not been entered.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: ComboBoxItem.pickerSaveButton

### Description
"Accept" button for [addUnknownValues:true](#attr-comboboxitemaddunknownvalues) ComboBoxItems showing the mobile interface.

The pickerSaveButton is an automatically created [NavigationButton](NavigationButton.md#class-navigationbutton) autoChild to dismiss the picker interface and store out the value entered in the [ComboBoxItem.pickerSearchField](#attr-comboboxitempickersearchfield), created when [ComboBoxItem.pickListPlacement](#attr-comboboxitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

This button will only be shown when [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) is true. Note that if a user has entered a partial known value, the pickList will show a filtered list of possible matches. An "Enter" keypress (or native keyboard "Done" button click on a mobile browser keyboard) will select the first match from the list. The pickerSaveButton provides a way for users to explicitly use the value as entered instead.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pickerSaveButtonTitle](#attr-comboboxitempickersavebuttontitle) for [Button.title](Button.md#attr-buttontitle)

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.optionOperationId

### Description
If this item has a specified `optionDataSource`, this attribute may be set to specify an explicit [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) when performing a fetch against the option dataSource to pick up display value mapping.

### Groups

- databinding

**Flags**: IR

---
## Attr: ComboBoxItem.addUnknownValues

### Description
This property controls whether the user can enter a value that is not present in the set of options for this item.

If set to false, the value the user enters in the text box is essentially used to filter the set of options displayed in the pickList.

In this mode, when focus is taken from the field, if the entered value does not match any entries in the [ValueMap](../reference_2.md#type-valuemap) or [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource), it will be discarded. Note that in this mode, [ComboBoxItem.completeOnTab](#attr-comboboxitemcompleteontab) behavior is automatically enabled so if the user enters a valid partial value such that one or more options is displayed in the pickList, and hits the Tab key, the first matching option will be chosen automatically. In this mode the user may also hit the `"Escape"` key to discard their edits.

Note also that when `addUnknownValues` is set to false, the underlying value returned by [getValue()](FormItem.md#method-formitemgetvalue) will not be updated until a value is explicitly chosen. This means any change or changed handlers will not fire directly in response to the user typing in the field - they will fire when the user actually selects a value, or takes focus from the field.

If this property is set to true, the user is not limited to entering values present in the set of options for the item. Instead the set of options essentially become a set of suggestions that may be used, or the user can enter an entirely new value.

**Flags**: IRW

---
## Attr: ComboBoxItem.maskSaveLiterals

### Description
Not applicable to a ComboBoxItem.

**Flags**: IRWA

---
## Attr: ComboBoxItem.separatorRows

### Description
Array of records to show between matching and non-matching rows in the PickList.

Not valid for [databound pickLists](#attr-comboboxitemoptiondatasource).

**Flags**: IR

---
## Attr: ComboBoxItem.pickerSearchField

### Description
The `pickerSearchField` is a separate [TextItem](TextItem.md#class-textitem) created for search string entry when [ComboBoxItem.pickListPlacement](#attr-comboboxitempicklistplacement) indicates that the search interface takes over an entire panel or the entire screen.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pickerSearchFieldHint](#attr-comboboxitempickersearchfieldhint) for [FormItem.hint](FormItem.md#attr-formitemhint)

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.showHintInField

### Description
If showing a hint for this form item, should it be shown within the field?

CSS style for the hint is [SelectItem.textBoxStyle](SelectItem.md#attr-selectitemtextboxstyle) with the suffix "Hint" appended to it.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)

**Flags**: IRW

---
## Attr: ComboBoxItem.fetchDisplayedFieldsOnly

### Description
If this item has a specified `optionDataSource` and this property is `true`, the list of fields used by this pickList will be passed to the datasource as [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs). If the datasource supports this feature the returned fields will be limited to this list. A custom datasource will need to add code to implement field limiting.

This list of used fields consists of the values of [valueField](FormItem.md#attr-formitemvaluefield), [displayField](FormItem.md#attr-formitemdisplayfield) and [pickListFields](#attr-comboboxitempicklistfields).

NOTE: When enabled, [getSelectedRecord](FormItem.md#method-formitemgetselectedrecord) will only include the fetched fields.

**Flags**: IRA

---
## Attr: ComboBoxItem.minimumSearchLength

### Description
Minimum length in characters before a search is performed. If too few characters are entered the pick list shows [searchStringTooShortMessage](#attr-comboboxitemsearchstringtooshortmessage).

**Flags**: IRA

---
## Attr: ComboBoxItem.allowExpressions

### Description
The standard [FormItem.allowExpressions](FormItem.md#attr-formitemallowexpressions) behavior is always disabled for ComboBoxItem.

The interface is not compatible with the `allowExpressions` feature. A ComboBoxItem normally starts fetching matches as you type, and that mixes very strangely with the idea of entering expressions like `"a..b"` - you will have the ComboBox seemingly switching back and forth between treating the text as a normal search string vs as a special expression on a per-keystroke basis.

We recommend a normal TextItem as the correct UI element to supply for users to enter filter expressions.

**Flags**: IRW

---
## Attr: ComboBoxItem.defaultValue

### Description
Static default value for this ComboBoxItem. To default to the first option use [ComboBoxItem.defaultToFirstOption](#attr-comboboxitemdefaulttofirstoption) instead.

**Flags**: IRW

---
## Attr: ComboBoxItem.initialSort

### Description
An array of [SortSpecifier](../reference.md#object-sortspecifier) objects used to set up the initial sort configuration for this pickList. If specified, this will be used instead of any [PickList.sortField](PickList.md#attr-picklistsortfield) specified.

### Groups

- sorting

**Flags**: IR

---
## Attr: ComboBoxItem.optionDataSource

### Description
If set, this FormItem will derive data to show in the PickList by fetching records from the specified `optionDataSource`. The fetched data will be used as a [valueMap](FormItem.md#attr-formitemvaluemap) by extracting the [valueField](FormItem.md#attr-formitemvaluefield) and [displayField](FormItem.md#attr-formitemdisplayfield) in the loaded records, to derive one valueMap entry per record loaded from the optionDataSource. Multiple fields from the fetched data may be shown in the pickList by setting [ComboBoxItem.pickListFields](#attr-comboboxitempicklistfields).

The data will be retrieved via a "fetch" operation on the DataSource, passing the [PickList.pickListCriteria](PickList.md#attr-picklistpicklistcriteria) (if set) as criteria, and passing [ComboBoxItem.optionFilterContext](#attr-comboboxitemoptionfiltercontext) (if set) as DSRequest Properties.

The fetch will be triggered when the pickList is first shown, or, you can set [autoFetchData:true](SelectItem.md#attr-selectitemautofetchdata) to fetch when the FormItem is first drawn.

The pickList will not re-fetch its options each time it is opened, unless the pickList criteria have changed. Developers who want to explicitly force a new fetch can achieve this by overriding [PickList.getPickListFilterCriteria](PickList.md#method-picklistgetpicklistfiltercriteria) to dynamically generate criteria that change whenever appropriate. For example, to force a new fetch every time the pickList is shown, the generated criteria could include a subcriterion for some arbitrary field with _operator_ `notEqual` and _value_ set to a something that will change each time the method runs, such as a date-stamp.

Note that providing an initial value when [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) is enabled, or enabling [defaultToFirstOption](SelectItem.md#attr-selectitemdefaulttofirstoption), can also cause a fetch to be initiated immediately upon form creation. You can also call [PickList.fetchData](PickList.md#method-picklistfetchdata) at any time to manually trigger a fetch.

Data paging is automatically enabled if the optionDataSource supports it. As the pickList is scrolled by the user, requests for additional data will be automatically issued.

For a pickList attached to a [ComboBoxItem](#class-comboboxitem), new fetches are issued as the user types, with criteria set as described under [ComboBoxItem.getPickListFilterCriteria](#method-comboboxitemgetpicklistfiltercriteria). If your dataSource is not capable of filtering results by search criteria (eg, the dataSource is backed by an XML flat file), you can set [ComboBoxItem.filterLocally](#attr-comboboxitemfilterlocally) to have the entire dataset loaded up front and filtering performed in the browser. This disables data paging.

Note that if a normal, static [valueMap](FormItem.md#attr-formitemvaluemap) is **also** specified for the field (either directly in the form item or as part of the field definition in the dataSource), it will be preferred to the data derived from the optionDataSource for whatever mappings are present.

**Flags**: IR

---
## Attr: ComboBoxItem.pickerSaveButtonTitle

### Description
The title for the [ComboBoxItem.pickerSaveButton](#attr-comboboxitempickersavebutton).

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.progressiveLoading

### Description
Indicates whether or not this ComboBoxItem will load its list of options [progressively](DataSource.md#attr-datasourceprogressiveloading). This property is copied onto the underlying [PickList](../reference_2.md#interface-picklist).

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)

**Flags**: IRW

---
## Attr: ComboBoxItem.showPickListOnKeypress

### Description
Should the list of options be displayed whenever the user types into the combo-box textArea, or only when the user clicks on the pick button or uses the explicit `Alt+Arrow Down` key combination?

**Flags**: IRW

---
## Attr: ComboBoxItem.pickListPlacement

### Description
Controls where the [PickList](../reference_2.md#interface-picklist) is placed. Can be specified as a [PanelPlacement](../reference_2.md#type-panelplacement) or a specific widget that should be filled (by specifying an actual Canvas or [Canvas.ID](Canvas.md#attr-canvasid)).

Default behavior is to `"fillPanel"` if [Browser.isHandset](Browser.md#classattr-browserishandset) or [Browser.isTablet](Browser.md#classattr-browseristablet), to better accommodate the smaller screen real estate and less precise pointing ability on such devices.

When filling the whole screen, part of the screen or a specific panel, the expanded interface is created as a [standard FormItem picker](FormItem.md#attr-formitempicker), and incorporates a [navigation bar](#attr-comboboxitempickernavigationbar) and [cancel button](#attr-comboboxitempickerexitbutton) that hides the expanded interface, as well as a separate [search field](#attr-comboboxitempickersearchfield).

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.pickerIconSrc

### Description
If [showPickerIcon](#attr-comboboxitemshowpickericon) is true for this item, this property governs the [src](FormItemIcon.md#attr-formitemiconsrc) of the picker icon image to be displayed.

When [spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) is enabled, this property will not be used to locate an image, instead, the image is drawn via CSS based on the [FormItem.pickerIconStyle](FormItem.md#attr-formitempickericonstyle) property.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: ComboBoxItem.pickerIconHeight

### Description
Don't specify an explicit height for the picker icon - instead have it size to match the height of the combo box item.

**Flags**: IRWA

---
## Attr: ComboBoxItem.separateSpecialValues

### Description
If true, [ComboBoxItem.specialValues](#attr-comboboxitemspecialvalues) special values such as the empty value will be shown in a separate non-scrolling area, in the [ComboBoxItem.separateValuesList](#attr-comboboxitemseparatevalueslist). Aside from making these values more easily accessible, showing them in a separate list allows data paging to be used, which is disabled if the separateValues are shown in the normal drop-down list along with other values.

**Flags**: IR

---
## Attr: ComboBoxItem.filterFields

### Description
As the user types into this item's textBox, a comboBoxItem will show the pick-list of options, and filter the set of results displayed by the current value in the text box. For a databound comboBoxItem, by default the entered value is filtered against the [displayField](#attr-comboboxitemdisplayfield) if one is specified, otherwise the [valueField](#attr-comboboxitemvaluefield).

This attribute allows the developer to explicitly change which fields to filter against, causing the user-entered text to be matched against any of the specified set of fields from the [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource).

This essentially causes [ComboBoxItem.getPickListFilterCriteria](#method-comboboxitemgetpicklistfiltercriteria) to return an [AdvancedCriteria](../reference.md#object-advancedcriteria) object representing "field1 starts with value or field2 starts with value or ...". The [operator](../reference.md#type-operatorid) used is controlled by [TextMatchStyle](../reference.md#type-textmatchstyle) as usual, that is, "startsWith" implies the operator "iStartsWith, "substring" implies "iContains" and "exact" implies "iEquals".

The most common use case for this setting would be when a comboBoxItem is showing multiple [ComboBoxItem.pickListFields](#attr-comboboxitempicklistfields) - if the same set of fields is specified as [ComboBoxItem.filterFields](#attr-comboboxitemfilterfields), the user can use the text-box to filter against whichever fields are visible in the pickList.

For finer grained control over comboBoxItem filtering, the [ComboBoxItem.getPickListFilterCriteria](#method-comboboxitemgetpicklistfiltercriteria) method may be overridden.

### Groups

- pickList

**Flags**: IR

---
## Attr: ComboBoxItem.pickerClearButtonTitle

### Description
The title for the [ComboBoxItem.pickerClearButton](#attr-comboboxitempickerclearbutton).

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.pickerClearButton

### Description
[NavigationButton](NavigationButton.md#class-navigationbutton) to clear the picker value, created when [ComboBoxItem.pickListPlacement](#attr-comboboxitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

This button will only be shown if [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) or [ComboBoxItem.allowEmptyValue](#attr-comboboxitemallowemptyvalue) is true.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [pickerClearButtonTitle](#attr-comboboxitempickerclearbuttontitle) for [Button.title](Button.md#attr-buttontitle)

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.iconPlacement

### Description
For PickList items with [PickListItemIconPlacement](../reference.md#type-picklistitemiconplacement) set such that the pickList does not render near-origin, should specified [icons](FormItem.md#attr-formitemicons) be rendered inline within the formItem itself, or within the [pickerNavigationBar](#attr-comboboxitempickernavigationbar).

May be overridden at the icon level via [FormItemIcon.iconPlacement](FormItemIcon.md#attr-formitemiconiconplacement).

For mobile browsing with limited available screen space, icons rendered in the navigation bar may be easier for the user to interact with.

**Flags**: IR

---
## Attr: ComboBoxItem.rootNodeId

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), this is the [id](SelectItem.md#attr-selectitemvaluefield) of the record to use as the [root](Tree.md#attr-treerootvalue) node.

**Flags**: IRW

---
## Attr: ComboBoxItem.pickList

### Description
ListGrid-based AutoChild created by the system to display a list of pickable options for this item.

The pickList is automatically generated and displayed by the system when necessary. It may be customized via properties such as [ComboBoxItem.pickListConstructor](#attr-comboboxitempicklistconstructor), [ComboBoxItem.pickTreeConstructor](#attr-comboboxitempicktreeconstructor), [ComboBoxItem.pickListProperties](#attr-comboboxitempicklistproperties) and more. See the [PickList overview](../reference_2.md#interface-picklist) for more information.

Accessing the generated pickList at runtime is an advanced usage. In most cases developers should not modify this generated component directly but should instead use attributes on the formItem to configure it.

**Flags**: RA

---
## Attr: ComboBoxItem.filterWithValue

### Description
Read-only property set by the ComboBoxItem to indicate whether we should use the current typed-in value as part of the filter criteria returned by [ComboBoxItem.getPickListFilterCriteria](#method-comboboxitemgetpicklistfiltercriteria). You can check this flag in order to mimic the ComboBoxItem's default behavior if you provide a custom implementation of `getPickListFilterCriteria()`.

### See Also

- [ComboBoxItem.getPickListFilterCriteria](#method-comboboxitemgetpicklistfiltercriteria)
- [ComboBoxItem.filterFields](#attr-comboboxitemfilterfields)

**Flags**: RA

---
## Attr: ComboBoxItem.showOptionsFromDataSource

### Description
If this item is part of a databound form, and has a specified `valueMap`, by default we show the valueMap options in the pickList for the item. Setting this property to true will ensure that the options displayed in our pickList are derived from the form's `dataSource`.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: ComboBoxItem.defaultToFirstOption

### Description
Select the first option as the default value for this ComboBoxItem. If options are derived from a dataSource, the first value returned by the server will be used, otherwise the first value in the valueMap. If enabled, this setting overrides [ComboBoxItem.defaultValue](#attr-comboboxitemdefaultvalue) and [ComboBoxItem.defaultDynamicValue](#method-comboboxitemdefaultdynamicvalue).

**Flags**: IRW

---
## Attr: ComboBoxItem.valueField

### Description
If this form item maps data values to display values by retrieving the [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) values from an [optionDataSource](FormItem.md#attr-formitemoptiondatasource), this property denotes the the field to use as the underlying data value in records from the optionDataSource.  
If not explicitly supplied, the valueField name will be derived as described in [FormItem.getValueFieldName](FormItem.md#method-formitemgetvaluefieldname).

### Groups

- databinding

**Flags**: IRW

---
## Attr: ComboBoxItem.specialValues

### Description
A set of "special" values such as "All", "None" or "Invalid" that do not appear in the normal [ValueMap](../reference_2.md#type-valuemap) or in the data returned by the [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource).

Like other uses of [ValueMap](../reference_2.md#type-valuemap), either a list of values or a mapping from stored to display value can be provided.

These values can either be shown at the top of the list of values (in the order specified), or can be shown in a separate, non-scrolling region - the setting [separateSpecialValues](SelectItem.md#attr-selectitemseparatespecialvalues) controls this. Note that data paging can only be used if `separateSpecialValues` is enabled.

If `specialValues` are configured, [allowEmptyValue](SelectItem.md#attr-selectitemallowemptyvalue) is ignored - an empty value, if desired, must be included in the `specialValues`. To provide a `specialValue` which clears the value of the field, use the special constant [PickList.emptyStoredValue](PickList.md#classattr-picklistemptystoredvalue).

`specialValues` can also be used to take a value that _does_ appear in the normal data and redundantly display it at the top of the list to make it more accessible. Note that in this case it is expected that the special value appears _both_ at the top of the list _and_ in it's normal position in the list, so this works best with [separateSpecialValues](SelectItem.md#attr-selectitemseparatespecialvalues) mode enabled.

Also, if an [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource) is used, [ComboBoxItem.specialValues](#attr-comboboxitemspecialvalues) that appear in the normal dataset _will_ be updated by automatic [cache synchronization](../reference.md#kb-topic-cachesync) (if the [ComboBoxItem.displayField](#attr-comboboxitemdisplayfield) is updated). However when using a distinct [ComboBoxItem.valueField](#attr-comboboxitemvaluefield) and [ComboBoxItem.displayField](#attr-comboboxitemdisplayfield), you are required to provide [ComboBoxItem.specialValues](#attr-comboboxitemspecialvalues) as a map (there is no support for [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) automatically fetching appropriate display values).

Note that specialValues are not supported in conjunction with [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem). Whereas with [selectItem.multiple:true](SelectItem.md#attr-selectitemmultiple), specialValues will never be normal values that may be selected. So, specialValues should have options such as "Select All", "Select None" and others.

**Flags**: IR

---
## Attr: ComboBoxItem.pickerSearchForm

### Description
Form that contains the [ComboBoxItem.pickerSearchField](#attr-comboboxitempickersearchfield).

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.saveOnEnter

### Description
ComboBox items will submit their containing form on enter keypress if [saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) is true. Setting this property to `false` will disable this behavior.

Note that if the drop down list of options (pickList) is visible an `Enter` keypress is used to select a value from the available set of options and will not automatically cause form submission.

**Flags**: IRW

---
## Attr: ComboBoxItem.showAllOptions

### Description
If true, even non-matching options will be shown, with configurable [separator rows](#attr-comboboxitemseparatorrows) in between. Not valid for [databound pickLists](#attr-comboboxitemoptiondatasource).

**Flags**: IR

---
## Attr: ComboBoxItem.pickerSearchOrNewValueFieldHint

### Description
[FormItem.hint](FormItem.md#attr-formitemhint) for the [ComboBoxItem.pickerSearchField](#attr-comboboxitempickersearchfield) when the combobox is configured to [allow unknown values](#attr-comboboxitemaddunknownvalues)

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.textMatchStyle

### Description
When applying filter criteria to pickList data, what type of matching to use.

For a databound pickList ([ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource) set), `textMatchStyle` is sent to the server as [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle).

For a non-databound pickList, `textMatchStyle` is applied by [filterClientPickListData()](PickList.md#method-picklistfilterclientpicklistdata).

**Flags**: IR

---
## Attr: ComboBoxItem.optionFilterContext

### Description
If this item has a specified `optionDataSource`, and this property is not null, this will be passed to the datasource as [DSRequest](../reference.md#object-dsrequest) properties when performing the filter operation on the dataSource to obtain the set of options for the list. This provides, among other capabilities, a way to trigger the server to return summary records.

### See Also

- [serverSummaries](../kb_topics/serverSummaries.md#kb-topic-server-summaries)

**Flags**: IRA

---
## Attr: ComboBoxItem.showPickerIcon

### Description
Should we show a special 'picker' [icon](../reference.md#object-formitemicon) for this form item? Picker icons are customizable via [pickerIconProperties](FormItem.md#attr-formitempickericonproperties). By default they will be rendered inside the form item's ["control box"](FormItem.md#attr-formitemcontrolstyle) area. By default clicking the pickerIcon will call [FormItem.showPicker](FormItem.md#method-formitemshowpicker).

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: ComboBoxItem.completeOnTab

### Description
If true, when the pickList is showing, the user can select the current value by hitting the `Tab` key.

Note that `completeOnTab` is not compatible with [ComboBoxItem.formatOnBlur](#attr-comboboxitemformatonblur)

**Flags**: IRW

---
## Attr: ComboBoxItem.autoOpenTree

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), which nodes should be opened automatically. Options are:

*   "none" - no nodes are opened automatically
*   "root" - opens the [top-level node](PickList.md#attr-picklistrootnodeid) - in databound tree-pickers, this node is always hidden
*   "all" - when [loading data on demand](ResultTree.md#attr-resulttreeloaddataondemand), opens the [top-level node](PickList.md#attr-picklistrootnodeid) and all of it's direct descendants - otherwise, opens all loaded nodes

**Flags**: IRW

---
## Attr: ComboBoxItem.singleClickFolderToggle

### Description
When this item is showing a [tree-based picker](PickList.md#attr-picklistdatasettype), the default behavior is for folder open-state to be toggled by double-clicking. Set this attribute to true to toggle folders on a single-click instead.

Note: when set to true, users can only choose leaf-nodes, since clicking folders would simply toggle them.

**Flags**: IRW

---
## Attr: ComboBoxItem.cachePickListResults

### Description
For databound pickLists (see [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)), by default SmartClient will cache and re-use datasets shown by different pickLists displayed by different SelectItems in an LRU (least recently used) caching pattern.

Setting this flag to false avoids this caching for situations where it is too aggressive.

Note that this does not control re-use of data **within a single pickList**. To control when client-side filtering is used in ComboBoxItem, see [ComboBoxItem.useClientFiltering](#attr-comboboxitemuseclientfiltering) and [ComboBoxItem.filterLocally](#attr-comboboxitemfilterlocally).

**Flags**: IR

---
## Attr: ComboBoxItem.pickerIconWidth

### Description
If [showPickerIcon](#attr-comboboxitemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: ComboBoxItem.pickerSearchFieldHint

### Description
[FormItem.hint](FormItem.md#attr-formitemhint) for the [ComboBoxItem.pickerSearchField](#attr-comboboxitempickersearchfield).

### Groups

- i18nMessages
- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.generateExactMatchCriteria

### Description
When a comboBoxItem is used to generate search criteria in a SearchForm this property governs whether, if the user explicitly chose an option from the pickList, we explicitly generate criteria that will search for an exact match against the chosen value.

In order to achieve this, when this property is set to true, this item will generate [AdvancedCriteria](../reference.md#object-advancedcriteria) in its [ComboBoxItem.getCriterion](#method-comboboxitemgetcriterion) method .

See [ComboBoxItem.shouldGenerateExactMatchCriteria](#method-comboboxitemshouldgenerateexactmatchcriteria) for behavior when this flag is unset.

**Flags**: IRWA

---
## Attr: ComboBoxItem.pickListProperties

### Description
If specified this properties block will be applied to the [pickList](PickListMenu.md#class-picklistmenu) created for this FormItem.

_Note_: Not every ListGrid property is supported when assigned to a pickList. Where there is a dedicated API on the form item (such as [pickListCellHeight](PickList.md#attr-picklistpicklistcellheight)), we recommend that be used in favor of setting the equivalent property on the `pickListProperties` block.

_PickLists and [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor):_  
[ComboBoxItems](#class-comboboxitem) do not support setting `showFilterEditor` to true on pickListProperties. This combination of settings leads to an ambiguous user experience as the two sets of filter-criteria (those from the text-box and those from the pickList filter editor) interact with each other.  
Setting [showFilterEditor:true](ListGrid_1.md#attr-listgridshowfiltereditor) in [SelectItem.pickListProperties](SelectItem.md#attr-selectitempicklistproperties) is a valid way to create a filterable pickList, on a SelectItem, but this setting is not supported on a SelectItem with [SelectItem.multiple](SelectItem.md#attr-selectitemmultiple) set to true - this combination of settings can cause a selected value to be filtered out of view at which point further selection changes will discard that value.  
In general we recommend the ComboBoxItem class (with [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) set as appropriate) as a better interface for filtering pickList data.

### Groups

- pickList

**Flags**: IRA

---
## Attr: ComboBoxItem.autoFetchData

### Description
If this combo box retrieves its options from a `dataSource`, should options be fetched from the server when the item is first written out, or should this fetch be delayed until the user opens the pickList.

### See Also

- [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)

**Flags**: IRA

---
## Attr: ComboBoxItem.dataSetType

### Description
Whether to show the picker as a flat list, or a collapsible tree.

The default value, "list", will use an instance of the [pickListConstructor](PickList.md#attr-picklistpicklistconstructor) as the picker - "tree" will show an instance of [pickTreeConstructor](PickList.md#attr-picklistpicktreeconstructor).

**Flags**: IR

---
## Attr: ComboBoxItem.formatOnBlur

### Description
With `formatOnBlur` enabled, this comboBoxItem will format its value according to the rules described in [FormItem.mapValueToDisplay](FormItem.md#method-formitemmapvaluetodisplay) as long as the item does not have focus. Once the user puts focus into the item the formatter will be removed. This provides a simple way for developers to show a nicely formatted display value in a freeform text field, without the need for an explicit [FormItem.formatEditorValue](FormItem.md#method-formitemformateditorvalue) and [FormItem.parseEditorValue](FormItem.md#method-formitemparseeditorvalue) pair.

Note that this attribute is not compatible with [ComboBoxItem.completeOnTab](#attr-comboboxitemcompleteontab)

**Flags**: IRW

---
## Attr: ComboBoxItem.maskPadChar

### Description
Not applicable to a ComboBoxItem.

**Flags**: IRWA

---
## Attr: ComboBoxItem.pickTreeConstructor

### Description
The Class to use when creating a picker of [type "tree"](PickList.md#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickTreeMenu](../reference.md#class-picktreemenu).

**Flags**: IR

---
## Attr: ComboBoxItem.allowEmptyValue

### Description
If [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) is `false`, this property determines whether the user can clear the comboBoxItem value, or whether they are constrained to choosing one of the available options (in which case clearing the text box will simply revert to the last picked value when the user leaves the field).

See also [ComboBoxItem.specialValues](#attr-comboboxitemspecialvalues) as a way of providing several different special values in addition to an empty value, such as "Invalid". Note that setting `specialValues` disables the use of `allowEmptyValue` - see details of how to have an empty value while using `specialValues` in in [the `specialValues` documentation](#attr-comboboxitemspecialvalues).

**Flags**: IR

---
## Attr: ComboBoxItem.pickListConstructor

### Description
The Class to use when creating a picker of [type "list"](PickList.md#attr-picklistdatasettype) for a FormItem. Must be a subclass of the builtin default, [PickListMenu](PickListMenu.md#class-picklistmenu).

### Groups

- pickList

**Flags**: IR

---
## Attr: ComboBoxItem.mask

### Description
Not applicable to a ComboBoxItem.

**Flags**: IRWA

---
## Attr: ComboBoxItem.pickerNavigationBar

### Description
[NavigationBar](NavigationBar.md#class-navigationbar) created when [ComboBoxItem.pickListPlacement](#attr-comboboxitempicklistplacement) indicates that the search interface takes over the entire panel or screen.

### Groups

- panelPlacement

**Flags**: IR

---
## Attr: ComboBoxItem.maskPromptChar

### Description
Not applicable to a ComboBoxItem.

**Flags**: IRWA

---
## Attr: ComboBoxItem.pickListFields

### Description
This property allows the developer to specify which field\[s\] will be displayed in the drop down list of options.

Only applies to databound pickLists (see [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource), or pickLists with custom data set up via the advanced [PickList.getClientPickListData](PickList.md#method-picklistgetclientpicklistdata) method.

If this property is unset, we display the [PickList.displayField](PickList.md#attr-picklistdisplayfield), if specified, otherwise the [PickList.valueField](PickList.md#attr-picklistvaluefield).

If there are multiple fields, column headers will be shown for each field, the height of which can be customized via the [PickList.pickListHeaderHeight](PickList.md#attr-picklistpicklistheaderheight) attribute.

Each field to display should be specified as a [ListGridField](../reference_2.md#object-listgridfield) object. Note that unlike in [listGrids](ListGrid_1.md#class-listgrid), dataSource fields marked as [hidden:true](DataSourceField.md#attr-datasourcefieldhidden) will be hidden by default in pickLists. To override this behavior, ensure that you specify an explicit value for [showIf](ListGridField.md#method-listgridfieldshowif).

### Groups

- pickList

### See Also

- [ComboBoxItem.valueField](#attr-comboboxitemvaluefield)
- [PickList.pickListHeaderHeight](PickList.md#attr-picklistpicklistheaderheight)

**Flags**: IRA

---
## Attr: ComboBoxItem.maskOverwriteMode

### Description
Not applicable to a ComboBoxItem.

**Flags**: IRWA

---
## Method: ComboBoxItem.getEnteredValue

### Description
Returns the raw text value that currently appears in the text field, which can differ from [FormItem.getValue](FormItem.md#method-formitemgetvalue) in various cases - for example:

*   for items that constrain the value range, such as a [DateItem](DateItem.md#class-dateitem) with [enforceDate](DateItem.md#attr-dateitemenforcedate):true, or a [ComboBoxItem](#class-comboboxitem) with [addUnknownValues](#attr-comboboxitemaddunknownvalues):false
*   for items with a defined valueMap or edit value formatter and parser functions which converts display value to data value
*   while the item has focus if [changeOnKeypress](TextItem.md#attr-textitemchangeonkeypress) is false

Note: if the pickList is being shown in any view other than the default [nearOrigin](#attr-comboboxitempicklistplacement), as is typically the case on a mobile device, this method will return the value of the [ComboBoxItem.pickerSearchField](#attr-comboboxitempickersearchfield).

### Returns

`[String](#type-string)` — current entered value

---
## Method: ComboBoxItem.shouldGenerateExactMatchCriteria

### Description
When a comboBoxItem is used to generate search criteria in a SearchForm, if the user explicitly chose an option from the pickList, should the criterion generated by [ComboBoxItem.getCriterion](#method-comboboxitemgetcriterion) enforce a search for an exact match against the chosen value?

In order to achieve this, when this property is set to true, this item will generate [AdvancedCriteria](../reference.md#object-advancedcriteria) in its [ComboBoxItem.getCriterion](#method-comboboxitemgetcriterion) method.

Default implementation will return [ComboBoxItem.generateExactMatchCriteria](#attr-comboboxitemgenerateexactmatchcriteria) if specified, otherwise true if the DataSource for this item [supports advanced criteria](DataSource.md#method-datasourcesupportsadvancedcriteria), false if it does not.

See [comboBoxItemCriteria](../kb_topics/comboBoxItemCriteria.md#kb-topic-comboboxitem-criteria) for a discussion of criterion generated by a ComboBoxItem.

### Returns

`[Boolean](#type-boolean)` — should getCriterion() generate exact-match search criteria when a value was explicitly chosen from this item's set of options?

**Flags**: A

---
## Method: ComboBoxItem.getClientPickListData

### Description
Returns the set of data to be displayed in this item's PickList.

This method will be called for non-databound form items implementing the PickList interface. The default implementation will derive data from the item's valueMap - can be overridden to allow a custom set of options to be displayed.

Note that for PickLists that filter data based on user input ([ComboBox](#class-comboboxitem)), this method should return the data **before filtering**. To customize the data returned after filtering, override [ComboBoxItem.filterClientPickListData](#method-comboboxitemfilterclientpicklistdata) instead.

As an example, for a formItem with [ComboBoxItem.valueField](#attr-comboboxitemvaluefield) set to "valueFieldName", the default implementation would take a valueMap like the following:

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

---
## Method: ComboBoxItem.getPickListFilterCriteria

### Description
[StringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview) to return filter criteria for options displayed for this item.

See [comboBoxFiltering](../kb_topics/comboBoxFiltering.md#kb-topic-comboboxitem-picklist-filtering) for details on how pickList filter criteria are calculated by default for a comboBoxItem.

### Returns

`[Criteria](../reference_2.md#type-criteria)` — criteria to be used for databound or local filtering

**Flags**: A

---
## Method: ComboBoxItem.hasAdvancedCriteria

### Description
Will this item return advancedCriteria if [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) is called on this item's form?

This method is overridden in ComboBoxItem to return true if [ComboBoxItem.shouldGenerateExactMatchCriteria](#method-comboboxitemshouldgenerateexactmatchcriteria) returns true, and the user has chosen an exact value from the options in the pickList. In this case we will use advancedCriteria to ensure the generated search criteria exactly matches the chosen value for this item.

As with formItem.hasAdvancedCriteria() this will also return true if an [Operator](../reference.md#object-operator) was explicitly specified for this item

See [comboBoxItemCriteria](../kb_topics/comboBoxItemCriteria.md#kb-topic-comboboxitem-criteria) for a discussion of criterion generated by a ComboBoxItem.

### Returns

`[Boolean](#type-boolean)` — true if the result of getCriterion() will be an AdvancedCriteria object.

### Groups

- criteriaEditing

---
## Method: ComboBoxItem.defaultDynamicValue

### Description
Expression evaluated to determine the [ComboBoxItem.defaultValue](#attr-comboboxitemdefaultvalue) when no value is provided for this item. To default to the first option use [ComboBoxItem.defaultToFirstOption](#attr-comboboxitemdefaulttofirstoption) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| values | [Object](../reference.md#type-object) | false | — | the current set of values for the form as a whole |

### Returns

`[Any](#type-any)` — dynamically calculated default value for this item

**Flags**: A

---
## Method: ComboBoxItem.fetchData

### Description
Only applies to databound items (see [PickList.optionDataSource](PickList.md#attr-picklistoptiondatasource)).  
Performs a fetch type operation on this item's DataSource to retrieve the set of valid options for the item, based on the current [PickList.pickListCriteria](PickList.md#attr-picklistpicklistcriteria).

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
## Method: ComboBoxItem.setCriterion

### Description
Overridden to support editing criterion against the display field or value field when [ComboBoxItem.addUnknownValues](#attr-comboboxitemaddunknownvalues) is true.

### Groups

- criteriaEditing

---
## Method: ComboBoxItem.getDisplayFieldName

### Description
Returns the `displayField` for this item.

Behavior varies based on the configuration of this item, as follows:

*   If this item has an [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource) and an explicit [FormItem.foreignDisplayField](FormItem.md#attr-formitemforeigndisplayfield) is specified, this will be returned.
*   Otherwise if an explicit [ComboBoxItem.displayField](#attr-comboboxitemdisplayfield) is specified it will be returned by default. If the `displayField` was specified on the underlying dataSource field, and no matching field is present in the [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource) for the item, we avoid returning the specified displayField value and instead return the title field of the option DataSource. We do this to avoid confusion for the case where the displayField is intended as a display-field value for showing another field value within the same record in the underlying dataSource only.
*   If no explicit foreignDisplay or displayField specification was found, and the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item is hidden in the [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this method will return the title field for the `optionDataSource`.

### Returns

`[FieldName](../reference.md#type-fieldname)` — display field name, or null if there is no separate display field to use.

**Flags**: A

---
## Method: ComboBoxItem.dataArrived

### Description
If this item is showing a dataBound pickList, this notification method will be fired when new data arrives from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | index of first row returned by the server |
| endRow | [int](../reference.md#type-int) | false | — | index of last row returned by the server |
| data | [ResultSet](#type-resultset) | false | — | pointer to this pickList's data |

---
## Method: ComboBoxItem.canEditCriterion

### Description
This method is overridden in comboBoxItem. When addUnknownValues is true, comboBoxItems allow the user to edit substring match type criteria applied to the display field (if one is specified).

The user can also edit criteria attempting to match exactly against the item's field name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | sub-criterion from an AdvancedCriteria object |

### Returns

`[boolean](../reference.md#type-boolean)` — return true if this item can edit the criterion in question.

### Groups

- criteriaEditing

---
## Method: ComboBoxItem.getCriterion

### Description
Returns criterion derived from the current value of this item.

See [comboBoxItemCriteria](../kb_topics/comboBoxItemCriteria.md#kb-topic-comboboxitem-criteria) for a discussion of criterion generated by a ComboBoxItem.

### Returns

`[Criterion](#type-criterion)` — criterion object based on this fields current edited value(s).

### Groups

- criteriaEditing

---
## Method: ComboBoxItem.getValueFieldName

### Description
Getter method to retrieve the [FormItem.valueField](FormItem.md#attr-formitemvaluefield) for this item. For items with a specified [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), this determines which field in that dataSource corresponds to the value for this item.

If unset, if a [foreignKey relationship](DataSourceField.md#attr-datasourcefieldforeignkey) exists between this field and the optionDataSource, this will be used, otherwise default behavior will return the [FormItem.name](FormItem.md#attr-formitemname) of this field.

### Returns

`[String](#type-string)` — fieldName to use a "value field" in records from this items [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource)

### Groups

- display_values

---
## Method: ComboBoxItem.getSelectedRecord

### Description
Get the record returned from the [ComboBoxItem.optionDataSource](#attr-comboboxitemoptiondatasource) when [fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) is true, and the missing value is fetched.

[FormItem.fetchMissingValues](FormItem.md#attr-formitemfetchmissingvalues) kicks off the fetch when the form item is initialized with a non null value or when setValue() is called on the item. Note that this method will return null before the fetch completes, or if no record is found in the optionDataSource matching the underlying value.

### Returns

`[ListGridRecord](#type-listgridrecord)` — selected record

### Groups

- display_values

---
## Method: ComboBoxItem.filterClientPickListData

### Description
Returns the data to display in the pick list.

The default implementation applies the criteria returned by [PickList.getPickListFilterCriteria](PickList.md#method-picklistgetpicklistfiltercriteria) to the data returned by [PickList.getClientPickListData](PickList.md#method-picklistgetclientpicklistdata). A record passes the filter if it has a matching value for all fields in the criteria object. Matching is performed according to [TextMatchStyle](../reference.md#type-textmatchstyle).

If [PickList.showAllOptions](PickList.md#attr-picklistshowalloptions) is set, all values are shown, with matching values shown below a [separator](PickList.md#attr-picklistseparatorrows).

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — array of record objects to display in the pickList

---
