# MultiSortPanel Documentation

[← Back to API Index](../reference.md)

---

## Class: MultiSortPanel

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A widget that allows the user to set up complex sorting arrangements by defining a group of [SortSpecifier](../reference.md#object-sortspecifier)s.

Each [SortSpecifier](../reference.md#object-sortspecifier) applies to a single property and direction - so, for instance, in a grid with two columns, `year` and `monthNumber`, you could sort first by `year` in descending order and then by `monthNumber` in ascending order. This would producing a grid sorted by year from largest (most recent) to smallest (least recent) and, within each year, by monthNumber from smallest (January) to largest (December).

---
## Attr: MultiSortPanel.otherSortLevelTitle

### Description
The title-text to appear in the first column for all sort-levels other than the first.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.iconSize

### Description
The size for the images in the [Level Up](#attr-multisortpanellevelupbutton) and [Level Down](#attr-multisortpanelleveldownbutton) buttons.

**Flags**: IR

---
## Attr: MultiSortPanel.addLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for adding new levels to the sort configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiSortPanel.addLevelButtonProperties` and `multiSortPanel.addLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortPanel.levelDownButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing sort-levels down in the sort configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiSortPanel.levelDownButtonProperties` and `multiSortPanel.levelDownButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortPanel.invalidListPrompt

### Description
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

Default value returns

``_Columns may only be used once: `[some field's title]` is used multiple times_``

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.maxLevels

### Description
The maximum number of levels of sorting that can be applied. Since each sort-property or field-name can be used only once in a given multi-sort operation, if no maxLevels value or a value larger than the total number of available properties is specified, it will default to the total number of available properties.

**Flags**: IR

---
## Attr: MultiSortPanel.fields

### Description
The list of fields which the user can choose to sort by.

**Flags**: IR

---
## Attr: MultiSortPanel.firstSortLevelTitle

### Description
The title-text to appear in the first column for the first sort-level.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.levelUpButtonTitle

### Description
The hover-prompt for the Level Up button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.propertyFieldTitle

### Description
The title-text to appear in the header of the "property" field.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.deleteLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for deleting levels from the sort configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiSortPanel.deleteLevelButtonProperties` and `multiSortPanel.deleteLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortPanel.descendingTitle

### Description
The title-text to appear in the "direction" field's SelectItem for a "descending" sort

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.copyLevelButtonTitle

### Description
The title-text to appear on the copyLevelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.optionsGrid

### Description
Automatically generated [ListGrid](ListGrid_1.md#class-listgrid) allowing the user to configure a set of [SortSpecifier](../reference.md#object-sortspecifier)s.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiSortPanel.optionsGridProperties` and `multiSortPanel.optionsGridDefaults`.

**Flags**: IR

---
## Attr: MultiSortPanel.ascendingTitle

### Description
The title-text to appear in the "direction" field's SelectItem for an "ascending" sort

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.copyLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for duplicating levels in the sort configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiSortPanel.copyLevelButtonProperties` and `multiSortPanel.copyLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortPanel.levelDownButtonTitle

### Description
The hover-prompt for the Level Down button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.levelUpButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing sort-levels up in the sort configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiSortPanel.levelUpButtonProperties` and `multiSortPanel.levelUpButtonDefaults`.

**Flags**: RA

---
## Attr: MultiSortPanel.addLevelButtonTitle

### Description
The title-text to appear on the addLevelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.directionFieldTitle

### Description
The title-text to appear in the header of the "direction" field.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.initialSort

### Description
The initial sort configuration to show in the [optionsGrid](#attr-multisortpaneloptionsgrid).

**Flags**: IR

---
## Attr: MultiSortPanel.deleteLevelButtonTitle

### Description
The title-text to appear on the deleteLevelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiSortPanel.iconBaseStyle

### Description
A CSS style to apply to images in the [Level Up](#attr-multisortpanellevelupbutton) and [Level Down](#attr-multisortpanelleveldownbutton) buttons. This is a base style supporting suffixes for states, specifically "Over", "Down" and "Disabled", which are applied when [ImgButton](ImgButton.md#class-imgbutton) settings like [ImgButton.showRollOverIcon](ImgButton.md#attr-imgbuttonshowrollovericon) are applied to the icons.

**Flags**: IR

---
## Method: MultiSortPanel.getSortLevel

### Description
Return a [SortSpecifier](../reference.md#object-sortspecifier) object for the requested levelNum.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| levelNum | [number](#type-number) | false | — | The index of the level to return a SortSpecifier for |

### Returns

`[SortSpecifier](#type-sortspecifier)` — A SortSpecifier representing the requested levelNum

---
## Method: MultiSortPanel.sortChanged

### Description
Fired whenever the sort configuration changes. The single parameter is an array of [SortSpecifier](../reference.md#object-sortspecifier)s that represent the list of sort-levels as they appear after whatever change has occurred.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortLevels | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | The current sort configuration, after any changes |

---
## Method: MultiSortPanel.getNumLevels

### Description
Return the number of levels of sorting that have been configured.

### Returns

`[number](#type-number)` — The number of levels of sorting that have been configured

---
## Method: MultiSortPanel.getSort

### Description
Returns all configured sorting levels, as an array of [SortSpecifier](../reference.md#object-sortspecifier)s.

### Returns

`[Array of SortSpecifier](#type-array-of-sortspecifier)` — the SortSpecifiers for all configured sorting levels

---
## Method: MultiSortPanel.validate

### Description
Validate that no two [SortSpecifier](../reference.md#object-sortspecifier)s sort on the same [property](../reference.md#attr-sortspecifierproperty).

### Returns

`[boolean](../reference.md#type-boolean)` — True if validation succeeds, false if any property is used twice

---
