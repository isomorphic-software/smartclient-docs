# SavedSearchItem Documentation

[← Back to API Index](../reference.md)

---

## Class: SavedSearchItem

*Inherits from:* [SelectItem](SelectItem.md#class-selectitem)

### Description
(SSI for short) Provides a UI for creating, editing and applying saved searches for a [target](#attr-savedsearchitemtargetcomponent) using the [SavedSearches](SavedSearches.md#class-savedsearches) system.

Normally, a `SavedSearchItem` is just provided a [targetComponent](#attr-savedsearchitemtargetcomponent), and all other configuration comes from the central [SavedSearches](SavedSearches.md#class-savedsearches) class by default. The `targetComponent` must be a [DataBoundComponent](../reference.md#interface-databoundcomponent) with a [DataSource configured](DataBoundComponent.md#attr-databoundcomponentdatasource).

Searches are applied to the target by calling [DataBoundComponent.fetchData](#method-databoundcomponentfetchdata), or, for ListGrids, by calling [ListGrid.setViewState](ListGrid_2.md#method-listgridsetviewstate). If [SavedSearchItem.saveLastSearch](#attr-savedsearchitemsavelastsearch) is set, the name of the last search is automatically stored in browser `localStorage`, and will be applied to the `targetComponent` as soon as saved searches are loaded.

By default, `SavedSearchItem` acquires the [default DataSource for storing searches](SavedSearches.md#attr-savedsearchesdefaultdatasource) and uses it as [SelectItem.optionDataSource](SelectItem.md#attr-selectitemoptiondatasource). The displayed value is the user's name for the search (from [SavedSearches.searchNameField](SavedSearches.md#attr-savedsearchessearchnamefield)) followed by a user-readable summary of the stored search, derived from [DataSource.getAdvancedCriteriaDescription](DataSource.md#classmethod-datasourcegetadvancedcriteriadescription), with a hover to show long values that may be clipped.

If [adding searches is allowed](#attr-savedsearchitemcanaddsearch), the `SavedSearchItem` either shows a [FormItemIcon](../reference.md#object-formitemicon) ([SavedSearchItem.addSearchIcon](#attr-savedsearchitemaddsearchicon)) or a pickList entry for adding searches ([SavedSearchItem.addSearchValue](#attr-savedsearchitemaddsearchvalue)). Either interface opens an [EditSearchWindow](../reference.md#class-editsearchwindow).

The [PickList](../reference_2.md#interface-picklist) is automatically configured to show the search name plus the search description (via [pickListFields](#attr-savedsearchitempicklistfields)), plus additional columns for icons for [editing](#attr-savedsearchitemeditsearchfield), [removal](#attr-savedsearchitemremovesearchfield), [copying existing searches](#attr-savedsearchitemcopysearchfield), and [choosing a default search](#attr-savedsearchitemmarkasdefaultfield).

Admin-configured searches are displayed after user-created searches, after a [separator](#attr-savedsearchitemadminseparatorrecord).

[SavedSearchItem.searchChanged](#method-savedsearchitemsearchchanged) fires when the user selects a new saved search, saves changes to an existing saved search, or saves a new search. Note that [valueField](SelectItem.md#attr-selectitemvaluefield) is set to [SavedSearches.componentIdField](SavedSearches.md#attr-savedsearchescomponentidfield) and [displayField](SelectItem.md#attr-selectitemdisplayfield) to [SavedSearches.searchNameField](SavedSearches.md#attr-savedsearchessearchnamefield).

Saving new searches also causes [SavedSearchItem.targetDataSource](#attr-savedsearchitemtargetdatasource) to be required. You can set [SavedSearchItem.newRecordValues](#attr-savedsearchitemnewrecordvalues) to a set of fixed values that should be saved whenever the user saves a new search; this can be used to save searches related to the current user's userId, for example.

The special interface that allows an admin to save shared searches appears if the user has the [SavedSearchItem.adminRole](#attr-savedsearchitemadminrole) as determined by [Authentication.hasRole](Authentication.md#classmethod-authenticationhasrole).

#### Saving full "viewState" for grids

If the [targetComponent](#attr-savedsearchitemtargetcomponent) is a [ListGrid](ListGrid_1.md#class-listgrid) or [TreeGrid](TreeGrid.md#class-treegrid), the default behavior is to store the complete [ListGrid.viewState](ListGrid_1.md#attr-listgridviewstate) rather that just search criteria. If you want to store just criteria, set [SavedSearchItem.storedState](#attr-savedsearchitemstoredstate) to "criteria".

**Note:** this feature requires [SmartClient Pro](https://www.smartclient.com/product/) or better.

---
## Attr: SavedSearchItem.copySearchField

### Description
ListGridField shown in the pickList to allow users to copy existing searches. The field is type "icon" and displays the skin's standard "copy" icon.

**Flags**: IR

---
## Attr: SavedSearchItem.hint

### Description
Text shown inside the field that serves as an indicator of what this field is for.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: SavedSearchItem.canEditSearch

### Description
Whether existing searches can be edited.

If no explicit value is set, it will be defaulted to `false` if the [target is a grid](#attr-savedsearchitemtargeteditscriteria). Searches can be edited by simply selecting them, using the grid's standard UI to edit the search, and then saving that as the original search.

**Flags**: IR

---
## Attr: SavedSearchItem.copySearchHoverText

### Description
Hover text that appeares over the +{copySearchField}

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.targetDataSource

### Description
DataSource that the saved searches are performed against.

Normally auto-derived from [targetComponent.dataSource](#attr-savedsearchitemtargetcomponent), but can be specified manually if no `targetComponent` is provided. In this case, [SavedSearchItem.searchChanged](#method-savedsearchitemsearchchanged) would be implement to apply criteria in a custom way.

**Flags**: IR

---
## Attr: SavedSearchItem.addSearchValue

### Description
Setting this property moves the [SavedSearchItem.canAddSearch](#attr-savedsearchitemcanaddsearch) functionality from an icon next to the form item ([SavedSearchItem.addSearchIcon](#attr-savedsearchitemaddsearchicon)) to the dropdown. When set, the SavedSearchItem will look for this value in [specialValues](SelectItem.md#attr-selectitemspecialvalues) and use it as the trigger action for [SavedSearchItem.canAddSearch](#attr-savedsearchitemcanaddsearch).

**Flags**: IR

---
## Attr: SavedSearchItem.saveLastSearch

### Description
If set, the name of the last search is automatically stored in browser `localStorage`, and will be applied to the `targetComponent` as soon as saved searches are loaded.

**Flags**: IR

---
## Attr: SavedSearchItem.editSearchHoverText

### Description
Hover text that appeares over the +{editSearchField}

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.canRemoveSearch

### Description
Whether existing searches can be removed.

**Flags**: IR

---
## Attr: SavedSearchItem.newRecordValues

### Description
Additional, fixed Record values that should be used every time a new search is saved.

This can be used to create user-specific saved searches by adding the userId as part of the saved Record's value.

Since this property is settable on the fly, you could also add an external interface that would allow a user to save system-wide searches that are not associated with their userId. For example, system-wide searches might have userId set to blank or to a special marker value, and the [SelectItem.optionCriteria](FormItem.md#attr-formitemoptioncriteria) could be set so that the `SavedSearchItem` shows system-wide as well as user-specific saved searches.

**Flags**: IRW

---
## Attr: SavedSearchItem.markAsAdminDefaultField

### Description
ListGridField shown in the pickList to allow admin users to designate which field is the admin-default search. The field is type "icon" and displays the skin's standard "checkbox" media.

**Flags**: IR

---
## Attr: SavedSearchItem.savedSearchDS

### Description
Optional override of [SavedSearches.defaultDataSource](SavedSearches.md#attr-savedsearchesdefaultdatasource) for this SavedSearchItem.

**Flags**: IR

---
## Attr: SavedSearchItem.confirmRemoval

### Description
Whether a confirmation message should be shown when a user removes a saved search. The message shown is the [SavedSearchItem.confirmRemovalMessage](#attr-savedsearchitemconfirmremovalmessage).

**Flags**: IR

---
## Attr: SavedSearchItem.targetComponent

### Description
Component that saved searches should apply to. May be specified as a DataBoundComponent instance or the String ID of one. When set, whenever [SavedSearchItem.searchChanged](#method-savedsearchitemsearchchanged) fires, the search is automatically applied to the `targetComponent` unless the `searchChanged` event is cancelled.

To avoid leaking local storage, saving searches will not be allowed for the target grid unless it specifies [savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid), or an explicit [local or global ID](Canvas.md#method-canvasgetlocalid) is present.

**Flags**: IR

---
## Attr: SavedSearchItem.title

### Description
Title of this FormItem. Mote that the title is hidden by default for SavedSearchItem.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.confirmRemovalMessage

### Description
Message shown when [removal confirmation](#attr-savedsearchitemconfirmremoval) is enabled and user attempts to remove a saved search. The variable "${title}" is available providing the display name of the saved search.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.markAsDefaultField

### Description
ListGridField shown in the pickList to allow users to designate which field is the default search. The field is type "icon" and displays the skin's standard "checkbox" media.

**Flags**: IR

---
## Attr: SavedSearchItem.addSearchIcon

### Description
Icon to be used to show the [EditSearchWindow](../reference.md#class-editsearchwindow).

**Flags**: IR

---
## Attr: SavedSearchItem.canAddSearch

### Description
This flag controls whether adding new searches is allowed.

**Flags**: IR

---
## Attr: SavedSearchItem.saveDefaultSearch

### Description
Works identically to [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch). The default is stored in browser `localStorage` using the [savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid) of the [SavedSearchItem.targetComponent](#attr-savedsearchitemtargetcomponent), or a combination of the [local or global ID](Canvas.md#method-canvasgetlocalid) and [DataSource ID](Class.md#method-classgetid) if no savedSearchId was specified (see documentation for [savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid) for details).

If no targetComponent is specified, the savedSearchId or minimal locator of the `SavedSearchItem` itself will be used.

Note that if the targetComponent is [ListGrid.autoFetchData](ListGrid_1.md#attr-listgridautofetchdata), and saveDefaultSearch is true, the SavedSearchItem automatically registers with the target component to prevent an automatic fetch with default criteria, and then, after looking up the default search, will perform either the default search or perform a standard autoFetch if no default search is found.

**Flags**: IR

---
## Attr: SavedSearchItem.removeSearchField

### Description
ListGridField shown in the pickList to allow users to remove existing searches. The field is type "icon" and displays the skin's standard "remove" icon.

An optional confirmation dialog is shown if [SavedSearchItem.confirmRemoval](#attr-savedsearchitemconfirmremoval) is set.

By default, if a record is an admin search (because it has no value for [SavedSearches.userIdField](SavedSearches.md#attr-savedsearchesuseridfield) or because [SavedSearches.adminField](SavedSearches.md#attr-savedsearchesadminfield) is true on the record), only an admin will be able to delete it.

Alternatively, if you are not using the `SavedSearchItem`'s admin features, specific records can be marked as unable to be removed via [SavedSearchItem.canModifyProperty](#attr-savedsearchitemcanmodifyproperty).

**Flags**: IR

---
## Attr: SavedSearchItem.savedSearchId

### Description
Optional explicit identifier for saved searches. See [SavedSearchItem.saveDefaultSearch](#attr-savedsearchitemsavedefaultsearch) for details.

**Flags**: IRA

---
## Attr: SavedSearchItem.editSearchField

### Description
ListGridField shown in the pickList to allow users to edit existing searches. The field is type "icon" and displays the skin's standard "edit" icon.

Does not appear if the [target is a grid](#attr-savedsearchitemtargeteditscriteria), since the simplest way of editing a search is just to select it, use the grid's built-in criteria editing to change it, and save as new.

Specific records can be marked as unable to be edited via [SavedSearchItem.canModifyProperty](#attr-savedsearchitemcanmodifyproperty).

**Flags**: IR

---
## Attr: SavedSearchItem.canCopySearch

### Description
Whether existing searches can be copied.

If no explicit value is set, it will be defaulted to `false` if the [target is a grid](#attr-savedsearchitemtargeteditscriteria). Searches can be copied by simply selecting them, using the grid's standard UI to edit the search, and then saving that as a new search.

**Flags**: IR

---
## Attr: SavedSearchItem.defaultSearchNameSuffix

### Description
HTML string to append to the search title in the search name field if this is the default search.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.editSearchWindow

### Description
Modal pop-up window shown when the user adds or edits a search, instance of of [EditSearchWindow](../reference.md#class-editsearchwindow).

**Flags**: IR

---
## Attr: SavedSearchItem.canModifyProperty

### Description
Optional name of a boolean field in the records returned by the `optionDataSource`, where setting the field to `false` means the Record cannot be edited or removed by the current user.

**Flags**: IR

---
## Attr: SavedSearchItem.storedState

### Description
Set to "criteria" if you want only criteria to be stored for ListGrids and TreeGrids instead of the full viewState of the component.

### See Also

- [SavedSearchItem](#class-savedsearchitem)

**Flags**: IR

---
## Attr: SavedSearchItem.markAsDefaultHoverText

### Description
Hover text that appeares over the +{markAsDefaultField}

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.adminRole

### Description
Role to check for (via [Authentication.hasRole](Authentication.md#classmethod-authenticationhasrole) to determine whether admin interfaces are shown. If not explicitly set, at initialization time this will be defaulted to [SavedSearches.adminRole](SavedSearches.md#attr-savedsearchesadminrole).

**Flags**: IRW

---
## Attr: SavedSearchItem.adminSeparatorRecord

### Description
Properties for the separator record between locally saved and admin searches.

**Flags**: IR

---
## Attr: SavedSearchItem.removeSearchHoverText

### Description
Hover text that appeares over the +{removeSearchField}

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.markAsAdminDefaultHoverText

### Description
Hover text that appeares over the +{markAsAdminDefaultField}

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchItem.targetEditsCriteria

### Description
Whether the [SavedSearchItem.targetComponent](#attr-savedsearchitemtargetcomponent) has built-in criteria editing or does not. True by default if the target is a [ListGrid](ListGrid_1.md#class-listgrid) or [TreeGrid](TreeGrid.md#class-treegrid) (but not [CubeGrid](CubeGrid.md#class-cubegrid)).

When the target has built-in criteria editing, the `SavedSearchItem` does not try to provide a [FilterBuilder](FilterBuilder.md#class-filterbuilder)-based criteria editing interface, so the [SavedSearchEditor](SavedSearchEditor.md#class-savedsearcheditor) is simplified to just allow naming of searches.

**Flags**: IR

---
## Attr: SavedSearchItem.offlineStorageKey

### Description
Optional key used for local storage of saved searches by this component.

If unset, the default [SavedSearches.offlineStorageKey](SavedSearches.md#attr-savedsearchesofflinestoragekey) will be used for local storage instead.

Has no effect if [SavedSearchItem.savedSearchDS](#attr-savedsearchitemsavedsearchds) is set.

**Flags**: IR

---
## Attr: SavedSearchItem.pickListFields

### Description
The SavedSearchItem pickListFields are automatically generated and contain fields for the search name plus the search description, plus additional columns for icons for editing, removal, copying existing searches, and choosing a default search.

**Flags**: RA

---
## Method: SavedSearchItem.searchChanged

### Description
Event fired whenever a user changes the currently selected saved search, modifies a saved search or adds a new saved search.

If a [SavedSearchItem.targetComponent](#attr-savedsearchitemtargetcomponent) has been specified, `searchChanged` automatically applies the new search to the `targetComponent` unless the event is cancelled by returning false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new criteria |
| searchData | [Record](#type-record) | false | — | savedSearch record |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to automatically apply the search to the [SavedSearchItem.targetComponent](#attr-savedsearchitemtargetcomponent)

---
## Method: SavedSearchItem.setTargetComponent

### Description
Changes the [SavedSearchItem.targetComponent](#attr-savedsearchitemtargetcomponent) to the passed in newTargetComponent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTargetComponent | [DataBoundComponent](#type-databoundcomponent) | false | — | the newTargetComponent |

---
