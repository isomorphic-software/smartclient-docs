# MultiSortDialog Documentation

[← Back to API Index](../main.md)

---

## Class: MultiSortDialog

*Inherits from:* [Window](Window.md#class-window)

### Description
A dialog that allows the user to set up complex sorting arrangements by defining a group of [SortSpecifier](../main_2.md#object-sortspecifier)s.

Each [SortSpecifier](../main_2.md#object-sortspecifier) applies to a single property and direction - so, for instance, in a grid with two columns, `year` and `monthNumber`, you could sort first by `year` in descending order and then by `monthNumber` in ascending order. This would producing a grid sorted by year from largest (most recent) to smallest (least recent) and, within each year, by monthNumber from smallest (January) to largest (December).

See [MultiSortDialog.askForSort](#classmethod-multisortdialogaskforsort), [DataBoundComponent.askForSort](DataBoundComponent.md#method-databoundcomponentaskforsort)

---
## Attr: MultiSortDialog.deleteLevelButton

### Description
Automatically generated [IButton](../main.md#class-ibutton) providing a mechanism for deleting levels from the sort configuration.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortPanel.deleteLevelButtonProperties` and `multiSortPanel.deleteLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortDialog.fields

### Description
The list of fields which the user can choose to sort by.

**Flags**: IR

---
## Attr: MultiSortDialog.title

### Description
The title-text to appear in this Dialog's Header-bar.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.levelDownButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing sort-levels down in the sort configuration.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortPanel.levelDownButtonProperties` and `multiSortPanel.levelDownButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortDialog.firstSortLevelTitle

### Description
The title-text to appear in the first column for the first sort-level.

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.applyButtonTitle

### Description
The title-text to appear on the applyButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.invalidListPrompt

### Description
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

Default value returns

``_Columns may only be used once: `[some field's title]` is used multiple times_``

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.applyButton

### Description
Automatically generated [IButton](../main.md#class-ibutton) providing the mechanism for accepting the current sort configuration. Fires the passed callback with a single parameter, sortLevels, representing the current sort configuration as an array of [SortSpecifier](../main_2.md#object-sortspecifier)s.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortDialog.applyButtonProperties` and `multiSortDialog.applyButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortDialog.levelUpButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing sort-levels up in the sort configuration.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortPanel.levelUpButtonProperties` and `multiSortPanel.levelUpButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortDialog.copyLevelButtonTitle

### Description
The title-text to appear on the copyLevelButton

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.optionsGrid

### Description
Automatically generated [ListGrid](ListGrid_1.md#class-listgrid) allowing the user to configure a set of [SortSpecifier](../main_2.md#object-sortspecifier)s.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortPanel.optionsGridProperties` and `multiSortPanel.optionsGridDefaults`.

**Flags**: IR

---
## Attr: MultiSortDialog.propertyFieldTitle

### Description
The title-text to appear in the header of the "property" field.

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.otherSortLevelTitle

### Description
The title-text to appear in the first column for all sort-levels other than the first.

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.initialSort

### Description
The initial sort configuration to show in the [optionsGrid](MultiSortPanel.md#attr-multisortpaneloptionsgrid).

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog.

**Flags**: IR

---
## Attr: MultiSortDialog.maxLevels

### Description
The maximum number of levels of sorting that can be applied. Since each sort-property or field-name can be used only once in a given multi-sort operation, if no maxLevels value or a value larger than the total number of available properties is specified, it will default to the total number of available properties.

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog.

**Flags**: IR

---
## Attr: MultiSortDialog.copyLevelButton

### Description
Automatically generated [IButton](../main.md#class-ibutton) providing a mechanism for duplicating levels in the sort configuration.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortPanel.copyLevelButtonProperties` and `multiSortPanel.copyLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortDialog.multiSortPanel

### Description
Automatically generated [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) displayed within this component.

**Flags**: R

---
## Attr: MultiSortDialog.cancelButton

### Description
Automatically generated [IButton](../main.md#class-ibutton) providing the mechanism for closing this Dialog without accepting the current sort configuration. The passed callback is fired with a single null parameter, indicating that the operation was cancelled.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortDialog.cancelButtonProperties` and `multiSortDialog.cancelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortDialog.addLevelButtonTitle

### Description
The title-text to appear on the addLevelButton.

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.cancelButtonTitle

### Description
The title-text to appear on the cancelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.descendingTitle

### Description
The title-text to appear in the "direction" field's SelectItem for a "descending" sort

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.deleteLevelButtonTitle

### Description
The title-text to appear on the deleteLevelButton

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.levelUpButtonTitle

### Description
The hover-prompt for the Level Up button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.directionFieldTitle

### Description
The title-text to appear in the header of the "direction" field.

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.levelDownButtonTitle

### Description
The hover-prompt for the Level Down button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.ascendingTitle

### Description
The title-text to appear in the "direction" field's SelectItem for an "ascending" sort

Note, this is a passthrough property which, when set, is passed through to the [MultiSortPanel](MultiSortPanel.md#class-multisortpanel) contained in this dialog. You only need to consider the properties on the MultiSortPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortDialog.addLevelButton

### Description
Automatically generated [IButton](../main.md#class-ibutton) providing a mechanism for adding new levels to the sort configuration.

This component is an [AutoChild](../main.md#type-autochild) and as such may be customized via `multiSortPanel.addLevelButtonProperties` and `multiSortPanel.addLevelButtonDefaults`.

**Flags**: RA

---
## ClassMethod: MultiSortDialog.askForSort

### Description
Launches a MultiSortDialog and obtains a sort-definition from the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldSource | [DataBoundComponent](#type-databoundcomponent)|[DataSource](#type-datasource)|[Array of DataSourceField](#type-array-of-datasourcefield) | false | — | A source for Fields which the user can choose to sort by |
| initialSort | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | The initial sort definition. |
| callback | [Callback](../main.md#type-callback) | false | — | Called when the user defines and accepts one or more [SortSpecifier](../main_2.md#object-sortspecifier)s. Single parameter `sortLevels` is an Array of SortSpecifier or null if the user cancelled the dialog. |
| properties | [MultiSortDialog Properties](#type-multisortdialog-properties) | true | — | Configuration to apply to the generated dialog |

---
## Method: MultiSortDialog.getNumLevels

### Description
Return the number of levels of sorting that have been configured.

### Returns

`[number](#type-number)` — The number of levels of sorting that have been configured

---
## Method: MultiSortDialog.validate

### Description
Validate that no two [SortSpecifier](../main_2.md#object-sortspecifier)s sort on the same [property](../main.md#attr-sortspecifierproperty).

### Returns

`[boolean](../main.md#type-boolean)` — True if validation succeeds, false if any property is used twice

---
## Method: MultiSortDialog.getSortLevel

### Description
Return a [SortSpecifier](../main_2.md#object-sortspecifier) object for the requested levelNum.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| levelNum | [number](#type-number) | false | — | The index of the level to return a SortSpecifier for |

### Returns

`[SortSpecifier](#type-sortspecifier)` — A SortSpecifier representing the requested levelNum

---
## Method: MultiSortDialog.getSort

### Description
Returns all configured sorting levels, as an array of [SortSpecifier](../main_2.md#object-sortspecifier)s.

### Returns

`[Array of SortSpecifier](#type-array-of-sortspecifier)` — the SortSpecifiers for all configured sorting levels

---
