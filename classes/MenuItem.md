# MenuItem Documentation

[← Back to API Index](../reference.md)

---

## Attr: MenuItem.keyTitle

### Description
A string to display in the shortcut-key column for this item. If not specified, the first KeyName value in [MenuItem.keys](#attr-menuitemkeys) will be used by default.

### Groups

- menuKeys

**Flags**: IR

---
## Attr: MenuItem.iconWidth

### Description
The width applied to this item's icon. The default of `16` can be changed for all MenuItems by overriding [Menu.iconWidth](Menu.md#attr-menuiconwidth).

### Groups

- menuIcons

**Flags**: IR

---
## Attr: MenuItem.canSelectParent

### Description
A MenuItem that has a submenu normally cannot be selected, instead clicking or hitting Enter while keyboard focus is on the item shows the submenu. Setting canSelectParent:true allows a menu item with a submenu to be selected directly.

**Flags**: IR

---
## Attr: MenuItem.title

### Description
The text displayed for the menu item

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.isSeparator

### Description
When set to `true`, this menu item shows a horizontal separator instead of the [MenuItem.title](#attr-menuitemtitle) text. Typically specified as the only property of a menu item, since the separator will not respond to mouse events.

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.autoDismiss

### Description
Whether a click on this specific `menuItem` automatically dismisses the menu. See [Menu.autoDismiss](Menu.md#attr-menuautodismiss).

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.embeddedComponentPosition

### Description
See [ListGridRecord.embeddedComponentPosition](ListGridRecord.md#attr-listgridrecordembeddedcomponentposition), except that when used in a `menuItem`, default behavior is [EmbeddedPosition](../reference_2.md#type-embeddedposition) "expand".

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.embeddedComponentFields

### Description
See [ListGridRecord.embeddedComponentFields](ListGridRecord.md#attr-listgridrecordembeddedcomponentfields). Default for a MenuItem is to cover the title and key fields, leaving the icon and submenu fields visible.

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.fetchSubmenus

### Description
If false, no submenus will be fetched for this MenuItem. This can be set globally via [Menu.fetchSubmenus](Menu.md#attr-menufetchsubmenus).

**Flags**: IR

---
## Attr: MenuItem.disabledIcon

### Description
The filename for this item's custom icon when the item is disabled. If both this property and [MenuItem.checked](#attr-menuitemchecked) are both specified, only the icon specified by this property will be displayed. The path to the loaded skin directory and the skinImgDir are prepended to this filename to form the full URL.

If you need to set this state dynamically, use [MenuItem.dynamicIcon](#method-menuitemdynamicicon) instead.

### Groups

- menuIcons

**Flags**: IR

---
## Attr: MenuItem.icon

### Description
The filename for this item's custom icon. If both this property and [MenuItem.checked](#attr-menuitemchecked) are both specified, only the icon specified by this property will be displayed. The path to the loaded skin directory and the skinImgDir are prepended to this filename to form the full URL. If this item is disabled, and [MenuItem.disabledIcon](#attr-menuitemdisabledicon) is set, then that icon will be used instead.

If you need to set this state dynamically, use [MenuItem.dynamicIcon](#method-menuitemdynamicicon) instead.

### Groups

- menuIcons

**Flags**: IR

---
## Attr: MenuItem.checked

### Description
If true, this item displays a standard checkmark image to the left of its title. You can set the checkmark image URL by setting [Menu.checkmarkImage](Menu.md#attr-menucheckmarkimage).

If you need to set this state dynamically, use [MenuItem.checkIf](#method-menuitemcheckif) instead.

### Groups

- menuIcons

**Flags**: IR

---
## Attr: MenuItem.enabled

### Description
Affects the visual style and interactivity of the menu item. If set to `false`, the menu item will not respond to mouse rollovers or clicks.

If you need to set this state dynamically, use [MenuItem.enableIf](#method-menuitemenableif) instead.

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.hidden

### Description
Default [Menu.itemHiddenProperty](Menu.md#attr-menuitemhiddenproperty) for menu items. If true, this item will be hidden wihin the menu by default.

To update item visibility at runtime, call [Menu.setItemHidden](Menu.md#method-menusetitemhidden)

### See Also

- [Menu.filterHiddenItems](Menu.md#attr-menufilterhiddenitems)

**Flags**: IR

---
## Attr: MenuItem.embeddedComponent

### Description
Arbitrary UI component that should appear in this MenuItem. See [ListGridRecord.embeddedComponent](ListGridRecord.md#attr-listgridrecordembeddedcomponent) for an overview and options for controlling placement.

When `embeddedComponent` is used in a MenuItem certain default behaviors apply:

*   [MenuItem.autoDismiss](#attr-menuitemautodismiss) defaults to false and clicks on embeddedComponents are not bubbled to the menuItem - if an interaction with an embeddedComponent is expected to dismiss the menu, custom code should call menu.[hide](Canvas.md#method-canvashide) or [hideAllMenus](Menu.md#classmethod-menuhideallmenus) as appropriate, before proceeding
*   the default behavior for [MenuItem.embeddedComponentPosition](#attr-menuitemembeddedcomponentposition) is "expand".
*   the component is placed over the title and key fields by default - use [MenuItem.embeddedComponentFields](#attr-menuitemembeddedcomponentfields) to override
*   rollOver styling is disabled by default (as though [ListGridRecord.showRollOver](ListGridRecord.md#attr-listgridrecordshowrollover) were set to false)

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.visibleWhen

### Description
Criteria to be evaluated to determine whether this MenuItem should be visible. Re-evaluated each time the menu is shown.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: MenuItem.iconHeight

### Description
The height applied to this item's icon. The default of `16` can be changed for all MenuItems by overriding [Menu.iconHeight](Menu.md#attr-menuiconheight).

### Groups

- menuIcons

**Flags**: IR

---
## Attr: MenuItem.enableWhen

### Description
Criteria to be evaluated to determine whether this MenuItem should be disabled. Re-evaluated each time the menu is shown.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: MenuItem.submenu

### Description
A reference to another menu, to display as a submenu when the mouse cursor hovers over this menu item.

### Groups

- menuBasic

**Flags**: IR

---
## Attr: MenuItem.keys

### Description
Shortcut key(s) to fire the menu item action. Each key can be defined as a [KeyIdentifier](../reference.md#object-keyidentifier). To apply multiple shortcut keys to this item, set this property to an array of such key identifiers.

### Groups

- menuKeys

**Flags**: IR

---
## Attr: MenuItem.showIconOnlyInline

### Description
When used in an [AdaptiveMenu](AdaptiveMenu.md#class-adaptivemenu), should this MenuItem show only it's [icon](#attr-menuitemicon) when displayed inline?

**Flags**: IR

---
## Method: MenuItem.enableIf

### Description
Contains the condition that will enable or disable the current menuItem. The handler must be specified as a function or string of script. Return false to disable the menuItem or true to enable it

If you don't need to set this state dynamically, use [MenuItem.enabled](#attr-menuitemenabled) instead.

Alternatively, you can use [Criteria](../reference_2.md#type-criteria) to declare when a MenuItem is enabled via [MenuItem.enableWhen](#attr-menuitemenablewhen).

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | [menu](Menu.md#class-menu) contains the reference to the menu that contains the current item |
| item | [MenuItem](#type-menuitem) | false | — | contains the reference to the current item |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true to show a checkmark by this menu item

### Groups

- dynamicMenuItem

---
## Method: MenuItem.action

### Description
Action to fire when this menu is activated.

### Groups

- menuBasic

---
## Method: MenuItem.dynamicTitle

### Description
Contains the condition that will change the current items' title when met. The handler must be specified as a function or string of script.

If you don't need to set this state dynamically, use [MenuItem.title](#attr-menuitemtitle) instead.

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | [menu](Menu.md#class-menu) contains the reference to the menu that contains the current item |
| item | [MenuItem](#type-menuitem) | false | — | contains the reference to the current item |

### Returns

`[String](#type-string)` — the title of this menuItem

### Groups

- dynamicMenuItem

---
## Method: MenuItem.dynamicIcon

### Description
Contains the condition that will change the current items' icon when met. The handler must be specified as a function or string of script.

If you don't need to set this state dynamically, use [MenuItem.icon](#attr-menuitemicon) instead.

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | [menu](Menu.md#class-menu) contains the reference to the menu that contains the current item |
| item | [MenuItem](#type-menuitem) | false | — | contains the reference to the current item |

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — the url of this menuItems icon

### Groups

- dynamicMenuItem

---
## Method: MenuItem.click

### Description
Executed when this menu item is clicked by the user. The click handler must be specified as a function or string of script. Return false to suppress the [Menu.itemClick](Menu.md#method-menuitemclick) handler if specified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | for a menu shown as a context menu, the Canvas the menu was shown on. Otherwise the [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member. |
| item | [MenuItem](#type-menuitem) | false | — | The [MenuItem](../reference_2.md#object-menuitem) that was clicked on. |
| menu | [Menu](#type-menu) | false | — | The [Menu](Menu.md#class-menu) instance of which this [MenuItem](../reference_2.md#object-menuitem) is a member. |
| colNum | [number](#type-number) | true | — | Index of the column the user clicked. May be null if the user activated the menu via a keyboard event. |

### Groups

- menuItemEvents

---
## Method: MenuItem.checkIf

### Description
Contains the condition that will check or uncheck the current menuItem. The handler must be specified as a function or string of script. Return false to uncheck the menuItem or true to check it

If you don't need to set this state dynamically, use [MenuItem.checked](#attr-menuitemchecked) instead.

May be defined as a [stringMethod](../kb_topics/stringMethods.md#kb-topic-string-methods-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | [target](Menu.md#attr-menutarget) attribute for the top level menu. |
| menu | [Menu](#type-menu) | false | — | [menu](Menu.md#class-menu) contains the reference to the menu that contains the current item |
| item | [MenuItem](#type-menuitem) | false | — | contains the reference to the current item |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true to show a checkmark by this menu item

### Groups

- dynamicMenuItem

---
