# AdaptiveMenuItem Documentation

[← Back to API Index](../reference.md)

---

## Method: AdaptiveMenuItem.checkIf

### Description
Contains the condition that will check or uncheck the current menuItem. The handler must be specified as a function or string of script. Return false to uncheck the menuItem or true to check it

If you don't need to set this state dynamically, use [MenuItem.checked](MenuItem.md#attr-menuitemchecked) instead.

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

Note that the `menu` parameter may be null if this `AdaptiveMenuItem` is not currently showing in a [Menu](Menu.md#class-menu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | The [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member, or null if this item is not currently displayed in a Menu |
| item | [AdaptiveMenuItem](#type-adaptivemenuitem) | false | — | contains the reference to the current item |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true to show a checkmark by this menu item

### Groups

- dynamicMenuItem

---
## Method: AdaptiveMenuItem.click

### Description
Executed when this menu item is clicked by the user. The click handler must be specified as a function or string of script. Return false to suppress the [Menu.itemClick](Menu.md#method-menuitemclick) handler if specified.

Note that the `menu` parameter may be null if this `AdaptiveMenuItem` is not currently showing in a [Menu](Menu.md#class-menu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | for a menu shown as a context menu, the Canvas the menu was shown on. Otherwise the [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member. |
| item | [MenuItem](#type-menuitem) | false | — | The [MenuItem](../reference_2.md#object-menuitem) that was clicked on. |
| menu | [Menu](#type-menu) | false | — | The [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member, or null if this item is not currently displayed in a Menu |
| colNum | [number](#type-number) | true | — | Index of the column the user clicked. May be null if the user activated the menu via a keyboard event. |

### Groups

- menuItemEvents

---
## Method: AdaptiveMenuItem.dynamicTitle

### Description
Contains the condition that will change the current items' title when met. The handler must be specified as a function or string of script.

If you don't need to set this state dynamically, use [MenuItem.title](MenuItem.md#attr-menuitemtitle) instead.

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

Note that the `menu` parameter may be null if this `AdaptiveMenuItem` is not currently showing in a [Menu](Menu.md#class-menu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | The [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member, or null if this item is not currently displayed in a Menu |
| item | [AdaptiveMenuItem](#type-adaptivemenuitem) | false | — | contains the reference to the current item |

### Returns

`[String](#type-string)` — the title of this menuItem

### Groups

- dynamicMenuItem

---
## Method: AdaptiveMenuItem.dynamicIcon

### Description
Contains the condition that will change the current items' icon when met. The handler must be specified as a function or string of script.

If you don't need to set this state dynamically, use [MenuItem.icon](MenuItem.md#attr-menuitemicon) instead.

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

Note that the `menu` parameter may be null if this `AdaptiveMenuItem` is not currently showing in a [Menu](Menu.md#class-menu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | The [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member, or null if this item is not currently displayed in a Menu |
| item | [AdaptiveMenuItem](#type-adaptivemenuitem) | false | — | contains the reference to the current item |

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — the url of this menuItems icon

### Groups

- dynamicMenuItem

---
## Method: AdaptiveMenuItem.getAdaptiveMenu

### Description
Return the [AdaptiveMenu](AdaptiveMenu.md#class-adaptivemenu) to which this item belongs

### Returns

`[AdaptiveMenu](#type-adaptivemenu)` — The AdaptiveMenu this item belongs to

### Groups

- menuItemEvents

---
## Method: AdaptiveMenuItem.enableIf

### Description
Contains the condition that will enable or disable the current menuItem. The handler must be specified as a function or string of script. Return false to disable the menuItem or true to enable it.

If you don't need to set this state dynamically, use [MenuItem.enabled](MenuItem.md#attr-menuitemenabled) instead.

Alternatively, you can use [Criteria](../reference_2.md#type-criteria) to declare when a MenuItem is enabled via [MenuItem.enableWhen](MenuItem.md#attr-menuitemenablewhen).

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

Note that the `menu` parameter may be null if this `AdaptiveMenuItem` is not currently showing in a [Menu](Menu.md#class-menu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | The [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member, or null if this item is not currently displayed in a Menu |
| item | [AdaptiveMenuItem](#type-adaptivemenuitem) | false | — | contains the reference to the current item |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true to show a checkmark by this menu item

### Groups

- dynamicMenuItem

---
