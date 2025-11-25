# SavedSearchEditor Documentation

[← Back to API Index](../main.md)

---

## Class: SavedSearchEditor

*Inherits from:* [VLayout](../main.md#class-vlayout)

### Description
User Interface component allowing a user to add a new saved search or edit an existing search. Automatically used by [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) and [ListGrid.canSaveSearches](ListGrid_1.md#attr-listgridcansavesearches); cannot be used directly and is documented only for skinning and internationalization purposes.

---
## Attr: SavedSearchEditor.cancelButton

### Description
Button used to cancel changes.

**Flags**: IR

---
## Attr: SavedSearchEditor.overwriteSharedSearchConfirmationMessage

### Description
Confirmation message to show when a user attempts to save a view with a searchName, componentID, and (if present) screenID / projectID which collides with another existing shared saved view.

This is the message that will be shown in a confirmation dialog if, for example, a user attempts to save a new view with the same name as an existing shared saved view for the same grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: SavedSearchEditor.validationFailedMessage

### Description
Notification message to show to the user in a warn dialog when an attempted save fails due to server validation error(s).

Validation errors will be appended to this string in the format _fieldName: errorMessage_.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: SavedSearchEditor.saveButton

### Description
Button used to save changes.

**Flags**: IR

---
## Attr: SavedSearchEditor.addSearchText

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchEditor.promptLabel

### Description
Label at the top of the interface, used to show instruction text, which is either [SavedSearchEditor.addSearchText](#attr-savedsearcheditoraddsearchtext) or [SavedSearchEditor.editSearchText](#attr-savedsearcheditoreditsearchtext) depending on whether the user is editing a pre-existing search.

For [grid mode](#attr-savedsearcheditormode), when adding a new search, the instructions text is [SavedSearchEditor.gridAddSearchText](#attr-savedsearcheditorgridaddsearchtext) instead.

**Flags**: IR

---
## Attr: SavedSearchEditor.isAdmin

### Description
Whether the editor is in admin mode, in which case the [SavedSearchEditor.sharedSearchCheckbox](#attr-savedsearcheditorsharedsearchcheckbox) appears to allow admins to define shared searches, and the [SavedSearchEditor.defaultSearchCheckbox](#attr-savedsearcheditordefaultsearchcheckbox) appears to enable an admin to designate a search as the (shared) default.

If [SavedSearches.adminRole](SavedSearches.md#attr-savedsearchesadminrole) is defined and [Authentication.hasRole](Authentication.md#classmethod-authenticationhasrole) indicates the current user has the `adminRole`, `isAdmin` is true by default, otherwise false.

**Flags**: IR

---
## Attr: SavedSearchEditor.overwriteSearchConfirmationMessage

### Description
Confirmation message to show when a user attempts to save a view with a searchName, componentID, and (if present) screenID / projectID which collides with another existing saved view.

This is the message that will be shown in a confirmation dialog if, for example, a user attempts to save a new view with the same name as an existing saved view for the same grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: SavedSearchEditor.filterBuilder

### Description
FilterBuilder used to enter criteria.

By default, [FilterBuilder.topOperatorAppearance](FilterBuilder.md#attr-filterbuildertopoperatorappearance) is set to "radio" (considered the simpler mode) and [FilterBuilder.showModeSwitcher](FilterBuilder.md#attr-filterbuildershowmodeswitcher) is set true.

If existing criteria cannot be displayed in simple ("radio") mode, advanced mode is automatically chosen.

**Flags**: IR

---
## Attr: SavedSearchEditor.sharedSearchTitle

### Description
Title for the [SavedSearchEditor.sharedSearchCheckbox](#attr-savedsearcheditorsharedsearchcheckbox).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchEditor.editSearchText

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchEditor.sharedSearchCheckbox

### Description
Checkbox shown when [SavedSearchEditor.isAdmin](#attr-savedsearcheditorisadmin) is true, allowing an admin to designate a search as an admin search that all users will see. Titled with [SavedSearchEditor.sharedSearchTitle](#attr-savedsearcheditorsharedsearchtitle).

**Flags**: IR

---
## Attr: SavedSearchEditor.mode

### Description
In "normal" the search editor shows a [FilterBuilder](FilterBuilder.md#class-filterbuilder) for editing criteria. In "grid" mode there is only a field for naming (or renaming) a search, since the grid has built-in interfaces for editing criteria.

**Flags**: IR

---
## Attr: SavedSearchEditor.searchNameItem

### Description
TextItem where the user enters the name for the saved search.

**Flags**: IR

---
## Attr: SavedSearchEditor.defaultSearchCheckbox

### Description
Checkbox shown when [SavedSearchEditor.isAdmin](#attr-savedsearcheditorisadmin) is true and the current search is marked as a shared search (via the [SavedSearchEditor.sharedSearchCheckbox](#attr-savedsearcheditorsharedsearchcheckbox)), allowing an admin to designate a search as the default search for users that have not chosen some other search as their default.

If checked, the [SavedSearches.setDefaultAdminSearchOperation](SavedSearches.md#attr-savedsearchessetdefaultadminsearchoperation) will be invoked after the search being edited has been saved. This will typically be invoked as a [queued request](RPCManager.md#classmethod-rpcmanagerstartqueue) in the same transaction that adds or updates the search being edited.

See the **Saving default searches** section of the [SavedSearches overview](SavedSearches.md#class-savedsearches) for more information on marking searches as a default.

Only ever appears if there is a [SavedSearches.adminDefaultField](SavedSearches.md#attr-savedsearchesadmindefaultfield) in the [SavedSearches.defaultDataSource](SavedSearches.md#attr-savedsearchesdefaultdatasource).

Titled with [SavedSearchEditor.defaultSearchTitle](#attr-savedsearcheditordefaultsearchtitle).

**Flags**: IR

---
## Attr: SavedSearchEditor.defaultSearchTitle

### Description
Title for the [SavedSearchEditor.sharedSearchCheckbox](#attr-savedsearcheditorsharedsearchcheckbox).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SavedSearchEditor.gridAddSearchText

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
