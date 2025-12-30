# MultiGroupDialog Documentation

[← Back to API Index](../reference.md)

---

## Class: MultiGroupDialog

*Inherits from:* [Window](Window.md#class-window)

### Description
A dialog that allows the user to set up complex grouping arrangements by defining a group of [GroupSpecifier](../reference.md#object-groupspecifier)s.

Each [GroupSpecifier](../reference.md#object-groupspecifier) applies to a single property and grouping - so, for instance, in a grid with two columns, `Nationhood` and `Country`, you could group first by `Nationhood` with its selected groupingMode and then by `Country` with its selected groupingMode.

_**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](../kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

---
## Attr: MultiGroupDialog.addLevelButtonTitle

### Description
The title-text to appear on the addLevelButton.

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog. You only need to consider the properties on the MultiGroupPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.applyButtonTitle

### Description
The title-text to appear on the applyButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.addLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for adding new levels to the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.addLevelButtonProperties` and `multiGroupPanel.addLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.applyButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing the mechanism for accepting the current group configuration. Fires the passed callback with a single parameter, groupLevels, representing the current group configuration as an array of [GroupSpecifier](../reference.md#object-groupspecifier)s.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.applyButtonProperties` and `multiGroupPanel.applyButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.deleteLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for deleting levels from the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.deleteLevelButtonProperties` and `multiGroupPanel.deleteLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.copyLevelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing a mechanism for duplicating levels in the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.copyLevelButtonProperties` and `multiGroupPanel.copyLevelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.maxLevels

### Description
The maximum number of levels of grouping that can be applied. Since each group-property or field-name can be used only once in a given multi-group operation, if no maxLevels value or a value larger than the total number of available properties is specified, it will default to the total number of available properties.

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog.

**Flags**: IR

---
## Attr: MultiGroupDialog.invalidListPrompt

### Description
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

Default value returns

``_Columns may only be used once: `[some field's title]` is used multiple times_``

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog. You only need to consider the properties on the MultiGroupPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.levelDownButtonTitle

### Description
The hover-prompt for the Level Down button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.title

### Description
The title-text to appear in this Dialog's Header-bar.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.initialGrouping

### Description
The initial group configuration to show in the [optionsGrid](MultiGroupPanel.md#attr-multigrouppaneloptionsgrid).

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog.

**Flags**: IR

---
## Attr: MultiGroupDialog.cancelButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) providing the mechanism for closing this Dialog without accepting the current group configuration. The passed callback is fired with a single null parameter, indicating that the operation was cancelled.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.cancelButtonProperties` and `multiGroupPanel.cancelButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.levelDownButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing group-levels down in the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.levelDownButtonProperties` and `multiGroupPanel.levelDownButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.copyLevelButtonTitle

### Description
The title-text to appear on the copyLevelButton

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog. You only need to consider the properties on the MultiGroupPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.levelUpButton

### Description
Automatically generated [ImgButton](ImgButton.md#class-imgbutton) providing a mechanism for moving existing group-levels up in the group configuration.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.levelUpButtonProperties` and `multiGroupPanel.levelUpButtonDefaults`.

**Flags**: RA

---
## Attr: MultiGroupDialog.optionsGrid

### Description
Automatically generated [ListGrid](ListGrid_1.md#class-listgrid) allowing the user to configure a set of [GroupSpecifier](../reference.md#object-groupspecifier)s.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `multiGroupPanel.optionsGridProperties` and `multiGroupPanel.optionsGridDefaults`.

**Flags**: IR

---
## Attr: MultiGroupDialog.propertyFieldTitle

### Description
The title-text to appear in the header of the "property" field.

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog. You only need to consider the properties on the MultiGroupPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.levelUpButtonTitle

### Description
The hover-prompt for the Level Up button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.deleteLevelButtonTitle

### Description
The title-text to appear on the deleteLevelButton

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog. You only need to consider the properties on the MultiGroupPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.cancelButtonTitle

### Description
The title-text to appear on the cancelButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.groupingFieldTitle

### Description
The title-text to appear in the header of the "property" field.

Note, this is a passthrough property which, when set, is passed through to the [MultiGroupPanel](MultiGroupPanel.md#class-multigrouppanel) contained in this dialog. You only need to consider the properties on the MultiGroupPanel for i18n.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiGroupDialog.fields

### Description
The list of fields which the user can choose to group by.

**Flags**: IR

---
## ClassMethod: MultiGroupDialog.askForGrouping

### Description
Launches a MultiGroupDialog and obtains a group-definition from the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldSource | [Array of Field](#type-array-of-field)|[DataSource](#type-datasource)|[DataBoundComponent](#type-databoundcomponent) | false | — | A source for Fields which the user can choose to group by |
| initialGrouping | [Array](#type-array) | false | — | The initial group definition. |
| callback | [Callback](../reference.md#type-callback) | false | — | Called when the user defines and accepts one or more [GroupSpecifier](../reference.md#object-groupspecifier)s. Single parameter `groupLevels` is an Array of GroupSpecifier or null if the user cancelled the dialog. |
| properties | [MultiGroupDialog Properties](#type-multigroupdialog-properties) | true | — | Configuration to apply to the generated dialog |

---
## Method: MultiGroupDialog.getNumLevels

### Description
Return the number of levels of grouping that have been configured.

### Returns

`[number](#type-number)` — The number of levels of grouping that have been configured

---
## Method: MultiGroupDialog.validate

### Description
Validate that no two [GroupSpecifier](../reference.md#object-groupspecifier)s group on the same [property](../reference.md#attr-groupspecifierproperty).

### Returns

`[boolean](../reference.md#type-boolean)` — True if validation succeeds, false if any property is used twice

---
## Method: MultiGroupDialog.getGroup

### Description
Returns all configured grouping levels, as an array of [GroupSpecifier](../reference.md#object-groupspecifier)s.

### Returns

`[Array of GroupSpecifier](#type-array-of-groupspecifier)` — the GroupSpecifiers for all configured grouping levels

---
