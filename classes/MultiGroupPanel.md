# MultiGroupPanel Documentation

[← Back to API Index](../reference.md)

---

## Class: MultiGroupPanel

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A widget that allows the user to set up complex grouping arrangements by defining a group of [GroupSpecifier](../reference.md#object-groupspecifier)s.

Each [GroupSpecifier](../reference.md#object-groupspecifier) applies to a single property and grouping - so, for instance, in a grid with two columns, `Nationhood` and `Country`, you could group first by `Nationhood` with its selected groupingMode and then by `Country` with its selected groupingMode. _**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](../kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

---
## Attr: MultiGroupPanel.levelDownButtonTitle

### Description
The hover-prompt for the Level Down button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.levelDownButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing group-levels down in the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.levelDownButtonProperties` and `multiGroupPanel.levelDownButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupPanel.invalidListPrompt

### Description
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

Default value returns

``_Columns may only be used once: `[some field's title]` is used multiple times_``

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.copyLevelButtonTitle

### Description
The title-text to appear on the copyLevelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.levelUpButtonTitle

### Description
The hover-prompt for the Level Up button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.groupingFieldTitle

### Description
The title-text to appear in the header of the "grouping" field.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.maxLevels

### Description
The maximum number of levels of grouping that can be applied. Since each group-property or field-name can be used only once in a given multi-group operation, if no maxLevels value or a value larger than the total number of available properties is specified, it will default to the total number of available properties.

**Flags**: IR

---
## Attr: MultiGroupPanel.deleteLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for deleting levels from the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.deleteLevelButtonProperties` and `multiGroupPanel.deleteLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupPanel.addLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for adding new levels to the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.addLevelButtonProperties` and `multiGroupPanel.addLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupPanel.otherGroupLevelTitle

### Description
The title-text to appear in the first column for all group-levels other than the first.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.deleteLevelButtonTitle

### Description
The title-text to appear on the deleteLevelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.firstGroupLevelTitle

### Description
The title-text to appear in the first column for the first group-level.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.propertyFieldTitle

### Description
The title-text to appear in the header of the "property" field.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.initialGrouping

### Description
The initial group configuration to show in the [optionsGrid](#attr-multigrouppaneloptionsgrid).

**Flags**: IR

---
## Attr: MultiGroupPanel.optionsGrid

### Description
Automatically generated [ListGrid](ListGrid_1.md#class-listgrid) allowing the user to configure a set of [GroupSpecifier](../reference.md#object-groupspecifier)s.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.optionsGridProperties` and `multiGroupPanel.optionsGridDefaults`.

**Flags**: IR

---
## Attr: MultiGroupPanel.addLevelButtonTitle

### Description
The title-text to appear on the addLevelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupPanel.fields

### Description
The list of fields which the user can choose to group by.

**Flags**: IR

---
## Attr: MultiGroupPanel.levelUpButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing group-levels up in the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.levelUpButtonProperties` and `multiGroupPanel.levelUpButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupPanel.copyLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for duplicating levels in the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.copyLevelButtonProperties` and `multiGroupPanel.copyLevelButtonDefaults`.

**Flags**: RA

---
## Method: MultiGroupPanel.groupChanged

### Description
Fired whenever the group configuration changes. The single parameter is an array of [GroupSpecifier](../reference.md#object-groupspecifier)s that represent the list of group-levels as they appear after whatever change has occurred.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupLevels | [Array of GroupSpecifier](#type-array-of-groupspecifier) | false | — | The current group configuration, after any changes |

---
## Method: MultiGroupPanel.validate

### Description
Validate that no two [GroupSpecifier](../reference.md#object-groupspecifier)s group on the same [property](../reference.md#attr-groupspecifierproperty).

### Returns

`[boolean](../reference.md#type-boolean)` — True if validation succeeds, false if any property is used twice

---
## Method: MultiGroupPanel.getGroup

### Description
Returns all configured grouping levels, as an array of [GroupSpecifier](../reference.md#object-groupspecifier)s.

### Returns

`[Array of GroupSpecifier](#type-array-of-groupspecifier)` — the GroupSpecifiers for all configured grouping levels

---
## Method: MultiGroupPanel.getNumLevels

### Description
Return the number of levels of grouping that have been configured.

### Returns

`[number](#type-number)` — The number of levels of grouping that have been configured

---
