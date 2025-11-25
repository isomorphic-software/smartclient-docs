# Menu Documentation

[← Back to API Index](../main.md)

---

## Class: Menu

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
The Menu widget class implements interactive menu widgets, with optional icons, submenus, and shortcut keys.

A Menu is initialized with a set of [MenuItem](../main_2.md#object-menuitem)s specified as [Menu.items](#attr-menuitems), each of which represents one row in the menu's display and specifies the action to take when that menu item is selected.

Each `MenuItem` can have a [title](MenuItem.md#attr-menuitemtitle), [icon](MenuItem.md#attr-menuitemicon), [shortcut keys](MenuItem.md#attr-menuitemkeys), optional [MenuItem.submenu](MenuItem.md#attr-menuitemsubmenu) and various other settings. Alternatively, a `MenuItem` can contain an arbitrary widget via [MenuItem.embeddedComponent](MenuItem.md#attr-menuitemembeddedcomponent).

To create a context menu for a component, provide a Menu instance for the [Canvas.contextMenu](Canvas.md#attr-canvascontextmenu) property. Note that some components like [ListGrid](ListGrid_1.md#class-listgrid) have more specific properties because they have distinct regions or because they have a default set of context menu actions available (for example: [ListGrid.headerContextMenu](ListGrid_1.md#attr-listgridheadercontextmenu) and related APIs).

If you want a button that pops up a menu when clicked, or a bar of such buttons, see the [MenuButton](MenuButton.md#class-menubutton) and [MenuBar](MenuBar.md#class-menubar) classes.

To create a pop-up panel interface that looks nothing like a `Menu` (but still dismisses automatically on an outside click), use [Canvas.showClickMask](Canvas.md#method-canvasshowclickmask) to arrange for automatic dismissal, and the [Canvas.showNextTo](Canvas.md#method-canvasshownextto) utility method to place the component near whatever triggered it, while automatically staying on-screen.

---
## Attr: Menu.baseStyle

### Description
CSS style for a normal cell

**Flags**: IRW

---
## Attr: Menu.target

### Description
Optional target canvas for this menu. Available as a parameter to dynamic menuItem configuration methods such as [MenuItem.checkIf](MenuItem.md#method-menuitemcheckif).

Whenever a Menu is shown as a contextMenu by a widget due to [Canvas.contextMenu](Canvas.md#attr-canvascontextmenu) being set, `menu.target` is automatically set to the widget that showed the contextMenu.

If this item has any [submenus](MenuItem.md#attr-menuitemsubmenu) the `target` will be propagated down to these child menus.

**Flags**: IRW

---
## Attr: Menu.canSaveSearches

### Description
Option to save searches is disabled for menus

**Flags**: IRA

---
## Attr: Menu.iconBodyStyleName

### Description
If set, the CSS style used for the body of this menu when there _is_ an icon field. In RTL mode, the `iconBodyStyleName` is suffixed with "RTL", which allows skins to apply different styles in LTR and RTL modes.

Note: Any skin which uses `iconBodyStyleName` should add "RTL" styles as well, even if identical to LTR styles. Otherwise, menus may lose their styling in RTL mode.

### Groups

- appearance

### See Also

- [Menu.iconFillSpaceStyleName](#attr-menuiconfillspacestylename)

**Flags**: IR

---
## Attr: Menu.fillSpaceStyleName

### Description
If set, alternative body style for the menu used when there is no icon field and the [Menu.placement](#attr-menuplacement) settings indicate the menu will be filling a portion of the screen or a panel. Generally this alternative style should not have rounded or excessively large edges. If unset, then [Menu.bodyStyleName](#attr-menubodystylename) is used instead.

When there is an icon field, [Menu.iconFillSpaceStyleName](#attr-menuiconfillspacestylename), if set, overrides this setting.

### Groups

- appearance

**Flags**: IR

---
## Attr: Menu.submenuFieldDefaults

### Description
Default properties for the automatically generated submenu column. Default object includes properties to set width, align and to show submenu icon for this column.

To modify the behavior or appearance of this column, developers may set [Menu.submenuFieldProperties](#attr-menusubmenufieldproperties) at the instance level, or override this object at the class level. If overriding this object, we recommend using [Class.changeDefaults](Class.md#classmethod-classchangedefaults) rather than replacing this object entirely.

See [Menu.showSubmenus](#attr-menushowsubmenus) for an overview of the submenu column.

**Flags**: IR

---
## Attr: Menu.placement

### Description
Where should the menu be placed on the screen?

Default is to use [PanelPlacement](../main_2.md#type-panelplacement) "fillScreen" if [Browser.isHandset](Browser.md#classattr-browserishandset). In any non-handset device, `placement` is unset, so the menu defaults to normal placement (near the originating MenuButton, or the mouse for a context menu, or according to left/top/width/height for a manually created Menu).

When using any `placement` setting that fills a portion of the screen or a panel, submenus are displayed by sliding them into place on top of the currently active menu, and a [menu.navigationBar](NavigationBar.md#class-navigationbar) is used to manage navigation to the main menu (and provide dismissal, via a [cancel button](#attr-menucancelbuttontitle).

**Flags**: IR

---
## Attr: Menu.submenuDisabledImage

### Description
Default image to use for the submenu indicator when the item is disabled. The value can be either a regular [SCImgURL](../main.md#type-scimgurl) which can specify _size:w,h;_, or an [ImgHTMLProperties](../main_2.md#object-imghtmlproperties) object, specifying at least _src_, _width_ and _height_.

If [Menu.submenuDirection](#attr-menusubmenudirection) is set to `"left"`, the image src will have the suffix `"_left"` appended to it.

**Flags**: IR

---
## Attr: Menu.filterHiddenItems

### Description
Does this hide menu items marked as [hidden menu items](MenuItem.md#attr-menuitemhidden) by filtering them out of the data set?

In order to support hiding items marked as hidden, if any items are hidden or marked with [visibleWhen rules](MenuItem.md#attr-menuitemvisiblewhen), Menus convert the specified [array of items](#attr-menudata) to a [FilteredList](FilteredList.md#class-filteredlist) with criteria set to filter out items marked with the [Menu.itemHiddenProperty](#attr-menuitemhiddenproperty).

Note that this means for `filterHiddenItems:true` menus, developers wishing to interact with the menu data set must use List APIs such as [menu.getData().getLength()](List.md#method-listgetlength) and [menu.getData().get(_index_)](List.md#method-listget), rather than accessing simple array attributes such as `menu.getData().length` or `menu.getData()[_index_]`

To get the full specified data set as an array, including hidden items, use [Menu.getAllItems](#method-menugetallitems).

**Flags**: IRA

---
## Attr: Menu.fetchSubmenus

### Description
When using a Tree or hierarchical DataSource as the menu's data, submenus are automatically generated from child nodes. `fetchSubmenus` can be set to false to disable this for the whole menu, or can be set false on a per-item basis via [MenuItem.fetchSubmenus](MenuItem.md#attr-menuitemfetchsubmenus).

**Flags**: IR

---
## Attr: Menu.navigationBar

### Description
Navigation bar shown when [Menu.placement](#attr-menuplacement) setting indicates that the menu should be shown filling a portion of the screen or a panel.

**Flags**: IR

---
## Attr: Menu.iconWidth

### Description
The default width applied to custom icons in this menu. This is used whenever item.iconWidth is not specified.

**Flags**: IRW

---
## Attr: Menu.items

### Description
Synonym for [Menu.data](#attr-menudata)

### Groups

- data

**Flags**: IRW

---
## Attr: Menu.dataProperties

### Description
For a `Menu` that uses a DataSource, these properties will be passed to the automatically-created ResultTree. This can be used for various customizations such as modifying the automatically-chosen [Tree.parentIdField](Tree.md#attr-treeparentidfield).

### Groups

- databinding

**Flags**: IR

---
## Attr: Menu.submenuConstructor

### Description
When using a Tree or hierarchical DataSource as the menu's data, optional subclass of Menu that should be used when generating submenus.

**Flags**: IR

---
## Attr: Menu.submenuImage

### Description
Default image to use for the submenu indicator. The value can be either a regular [SCImgURL](../main.md#type-scimgurl) which can specify _size:w,h;_, or an [ImgHTMLProperties](../main_2.md#object-imghtmlproperties) object, specifying at least _src_, _width_ and _height_.

If [Menu.submenuDirection](#attr-menusubmenudirection) is set to `"left"`, the image src will have the suffix `"_left"` appended to it.

**Flags**: IR

---
## Attr: Menu.initialCriteria

### Description
Criteria to be used when fetching items for this Menu. Note that [setCriteria](ListGrid_2.md#method-listgridsetcriteria) is not supported in Menus.

### Groups

- databinding

**Flags**: IR

---
## Attr: Menu.useKeys

### Description
A boolean indicating whether this menu should use shortcut keys. Set useKeys to false in a menu's initialization block to explicitly disable shortcut keys.

**Flags**: IRW

---
## Attr: Menu.showSubmenus

### Description
A boolean, indicating whether the submenu indicator column should be displayed. If showSubmenus is not set, the menu will show the indicator column only if one of its items specifies a submenu property. If showSubmenus is false, the submenu arrows will not be displayed, but submenus will still appear on rollover.

**Flags**: IRW

---
## Attr: Menu.iconFieldProperties

### Description
Custom properties for the automatically generated icon column.

See [Menu.showIcons](#attr-menushowicons) for an overview of the icon column.

**Flags**: IR

---
## Attr: Menu.canShowFilterEditor

### Description
Option to show filter editor is disabled for menus

**Flags**: IRA

---
## Attr: Menu.showEdges

### Description
`showEdges` dynamically defaults to false when the [Menu.placement](#attr-menuplacement) setting indicates the Menu will be filling a portion of the screen or a panel.

**Flags**: IR

---
## Attr: Menu.autoFetchData

### Description
This DataBoundComponent attribute is non-functional in Menus, where fetches are always automatic.

### Groups

- databinding

**Flags**: IR

---
## Attr: Menu.cellHeight

### Description
The height of each item in the menu, in pixels.

### Groups

- sizing
- sizing

**Flags**: IRW

---
## Attr: Menu.navStack

### Description
When the [Menu.placement](#attr-menuplacement) setting indicates that the menu should be shown filling a portion of the screen or a panel, `navStack` is a container element created to hold the [NavigationBar](NavigationBar.md#class-navigationbar) and any submenus that are shown by the menu.

**Flags**: IR

---
## Attr: Menu.emptyMessage

### Description
Message to show when a menu is shown with no items.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: Menu.iconHeight

### Description
The default height applied to custom icons in this menu. This is used whenever item.iconHeight is not specified.

**Flags**: IRW

---
## Attr: Menu.defaultWidth

### Description
The default menu width.

### Groups

- sizing

**Flags**: IRW

---
## Attr: Menu.canSelectParentItems

### Description
If true, clicking or pressing Enter on a menu item that has a submenu will select that item (with standard behavior of hiding the menus, calling click handlers, etc) instead of showing the submenu.

### Groups

- selection

**Flags**: IRW

---
## Attr: Menu.fields

### Description
Array of columns to show for this menu.  
Standard menu fields may be included by specifying [MenuFieldIDs](../main.md#type-menufieldid) directly. Additional custom fields may be specified as [ListGridField](../main_2.md#object-listgridfield) objects.  
If this property is unset, default behavior will show the [standard set of fields](../main.md#type-menufieldid), with the exception of any that have been suppressed via [Menu.showIcons](#attr-menushowicons), [Menu.showKeys](#attr-menushowkeys) and [Menu.showSubmenus](#attr-menushowsubmenus)

**Flags**: IRWA

---
## Attr: Menu.showShadow

### Description
Whether to show a drop shadow for this Canvas.

Developers should be aware that the drop shadow is drawn outside the specified width and height of the widget meaning a widget with shadows takes up a little more space than it otherwise would. A full screen canvas with showShadow set to true as this would be likely to cause browser scrollbars to appear - developers can handle this by either setting this property to false on full-screen widgets, or by setting overflow to "hidden" on the `<body>` element browser-level scrolling is never intended to occur.

`showShadow` dynamically defaults to false when the [Menu.placement](#attr-menuplacement) setting indicates the Menu will be filling a portion of the screen or a panel.

**Flags**: IR

---
## Attr: Menu.iconFillSpaceStyleName

### Description
If set, alternative body style for the menu used when there is an icon field and the [Menu.placement](#attr-menuplacement) settings indicate the menu will be filling a portion of the screen or a panel. Generally this alternative style should not have rounded or excessively large edges. In RTL mode, the `iconFillSpaceStyleName` is suffixed with "RTL", which allows skins to apply different styles in LTR and RTL modes. If unset, then [Menu.iconBodyStyleName](#attr-menuiconbodystylename) is used instead.

Note: Like `iconBodyStyleName`, any skin which uses `iconFillSpaceStyleName` should add "RTL" styles as well, even if identical to LTR styles. Otherwise, menus may lose their styling in RTL mode.

### Groups

- appearance

**Flags**: IR

---
## Attr: Menu.cascadeAutoDismiss

### Description
When true any generated submenus will inherit [Menu.autoDismiss](#attr-menuautodismiss) from this menu.

**Flags**: IRW

---
## Attr: Menu.cancelButtonTitle

### Description
Title for the "Done" button shown when the [NavigationBar](NavigationBar.md#class-navigationbar) is present.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: Menu.autoDraw

### Description
Menus will not draw on initialization, until they're explicitly show()n

**Flags**: IRWA

---
## Attr: Menu.showIcons

### Description
A boolean, indicating whether the checkmark/custom icon column should be displayed.

**Flags**: IRW

---
## Attr: Menu.data

### Description
An array of menuItem objects, specifying the menu items this menu should show.

Data may also be set to a [Tree](Tree.md#class-tree) in which case a hierarchy of menus and submenus will automatically be generated to match the tree structure. See also [Menu.dataSource](#attr-menudatasource) for dynamically fetching menuItems and submenus from a hierarchical DataSource.

Note that items that are marked as [hidden](MenuItem.md#attr-menuitemhidden) will be automatically filtered out of the data dispayed to the user. To retrieve the full set of items at runtime, including hidden items, use [Menu.getAllItems](#method-menugetallitems).

### Groups

- data

**Flags**: IRW

---
## Attr: Menu.autoDismiss

### Description
When false, when a menu item is chosen (via mouse click or keyboard), the menu is not automatically hidden, staying in place for further interactivity

### See Also

- [Menu.cascadeAutoDismiss](#attr-menucascadeautodismiss)

**Flags**: IRW

---
## Attr: Menu.dataSource

### Description
Optional DataSource to fetch menuItems and submenus from, instead of using [Menu.items](#attr-menuitems).

Data is tree-based in menus, so the provided DataSource should be set up for hierarchical fetching - see the [Tree Data Binding overview](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding).

Note that, although Menu is a subclass of [ListGrid](ListGrid_1.md#class-listgrid), some APIs, like [setCriteria](ListGrid_2.md#method-listgridsetcriteria) and [autoFetchData](ListGrid_1.md#attr-listgridautofetchdata) are not supported in menus. If a dataSource is supplied, it is automatically fetched against as required, without the need for autoFetchData. To apply criteria to the fetches made in this way, see [initialCriteria](#attr-menuinitialcriteria).  
Moreover, fetchData() is also an example of a ListGrid API that doesn't apply to menu, and, as was done for setCriteria() and other APIs like setCriteria().

**Flags**: IR

---
## Attr: Menu.submenuDirection

### Description
Should submenus show up on our left or right. Can validly be set to `"left"` or `"right"`. If unset, submenus show up on the right by default in Left-to-right text mode, or on the left in Right-to-left text mode (see [Page.isRTL](Page.md#classmethod-pageisrtl)).

**Flags**: IRW

---
## Attr: Menu.keyFieldProperties

### Description
Custom properties for the automatically generated key column.

See [Menu.showKeys](#attr-menushowkeys) for an overview of the key column.

**Flags**: IR

---
## Attr: Menu.alternateRecordStyles

### Description
Explicitly disable alternateRecordStyles at the menu level by default so setting to true for all ListGrids will not impact menus' appearance.

**Flags**: IRW

---
## Attr: Menu.checkmarkDisabledImage

### Description
Default image to display for [check-marked items](MenuItem.md#attr-menuitemchecked) when the item is disabled. The value can be either a regular [SCImgURL](../main.md#type-scimgurl) which can specify _size:w,h;_, or an [ImgHTMLProperties](../main_2.md#object-imghtmlproperties) object, specifying at least _src_, _width_ and _height_.

**Flags**: IR

---
## Attr: Menu.iconFieldDefaults

### Description
Default properties for the automatically generated icon column. Default object includes properties to set width and to show icon for this column.

To modify the behavior or appearance of this column, developers may set [Menu.iconFieldProperties](#attr-menuiconfieldproperties) at the instance level, or override this object at the class level. If overriding this object, we recommend using [Class.changeDefaults](Class.md#classmethod-classchangedefaults) rather than replacing this object entirely.

See [Menu.showIcons](#attr-menushowicons) for an overview of the icon column.

**Flags**: IR

---
## Attr: Menu.itemHiddenProperty

### Description
Items with this property set to true will be hidden within the menu.

### See Also

- [Menu.filterHiddenItems](#attr-menufilterhiddenitems)

**Flags**: IRWA

---
## Attr: Menu.showKeys

### Description
A boolean, indicating whether the shortcut key column should be displayed. If showKeys is not set, the menu will show the key column only if one of its items specifies a keys property. If showKeys is false, the keys will not be displayed, but will still function.

**Flags**: IRW

---
## Attr: Menu.showAnimationEffect

### Description
When this menu is shown how should it animate into view? By default the menu will just show at the specified size/position. Options for animated show effects are `"fade"` to fade from transparent to visible, `"slide"` to slide the menu into view, or `"wipe"` to have the menu grow into view, revealing its content as it grows. Can be overridden by passing the 'animationEffect' parameter to 'menu.show()'

**Flags**: IRWA

---
## Attr: Menu.keyFieldDefaults

### Description
Default properties for the automatically generated key column. Default object includes properties to set width and to show key for this column.

To modify the behavior or appearance of this column, developers may set [Menu.keyFieldProperties](#attr-menukeyfieldproperties) at the instance level, or override this object at the class level. If overriding this object, we recommend using [Class.changeDefaults](Class.md#classmethod-classchangedefaults) rather than replacing this object entirely.

See [Menu.showKeys](#attr-menushowkeys) for an overview of the key column.

**Flags**: IR

---
## Attr: Menu.bodyStyleName

### Description
CSS style used for the body of this menu when there is no icon field. When there is an icon field, then [iconBodyStyleName](#attr-menuiconbodystylename), if set, will override this setting.

If applying a background-color to the body via a CSS style applied using this property, be sure to set [bodyBackgroundColor](ListGrid_1.md#attr-listgridbodybackgroundcolor) to `null`.

### Groups

- appearance

### See Also

- [Menu.fillSpaceStyleName](#attr-menufillspacestylename)

**Flags**: IRW

---
## Attr: Menu.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Menu.menuButtonWidth

### Description
For a menu that has a [MenuButton](MenuButton.md#class-menubutton) generated for it automatically (for example when included in a [MenuBar](MenuBar.md#class-menubar), the width that the MenuButton should have. If unset, the MenuButton will be as wide as `menu.width`.

**Flags**: IR

---
## Attr: Menu.autoDismissOnBlur

### Description
When false, when a user clicks outside the menu, or hits the Escape key, this menu will not be automatically hidden, staying in place for further interactivity.

**Flags**: IRW

---
## Attr: Menu.titleFieldDefaults

### Description
Default properties for the automatically generated title column. Default object includes properties to set width and to show title for this column.

To modify the behavior or appearance of this column, developers may set [Menu.titleFieldProperties](#attr-menutitlefieldproperties) at the instance level, or override this object at the class level. If overriding this object, we recommend using [Class.changeDefaults](Class.md#classmethod-classchangedefaults) rather than replacing this object entirely.

**Flags**: IR

---
## Attr: Menu.submenuFieldProperties

### Description
Custom properties for the automatically generated submenu column.

See [Menu.showSubmenus](#attr-menushowsubmenus) for an overview of the submenu column.

**Flags**: IR

---
## Attr: Menu.titleFieldProperties

### Description
Custom properties for the automatically generated title column.

**Flags**: IR

---
## Attr: Menu.checkmarkImage

### Description
Default image to display for [check-marked items](MenuItem.md#attr-menuitemchecked). The value can be either a regular [SCImgURL](../main.md#type-scimgurl) which can specify _size:w,h;_, or an [ImgHTMLProperties](../main_2.md#object-imghtmlproperties) object, specifying at least _src_, _width_ and _height_.

**Flags**: IR

---
## ClassMethod: Menu.hideAllMenus

### Description
Hide all menus that are currently open. This method is useful to hide the current set of menus including submenus, and dismiss the menu's clickMask.

---
## Method: Menu.setItemEnabled

### Description
Enables or disables the menu item according to the value of newState, and redraws the menu if necessary. Returns true if there's a change in the enabled state.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[int](../main.md#type-int) | false | — | MenuItem or visible index of the MenuItem |
| newState | [boolean](../main.md#type-boolean) | true | — | true to enable the menu item, false to disable it. If not passed, true is assumed |

### Returns

`[boolean](../main.md#type-boolean)` — true if the enabled state was changed

---
## Method: Menu.getVisibleItemNum

### Description
Given a MenuItem, return its index in the currently visible set of items.

To get the index of the item in the [full set of items](#method-menugetallitems), including [hidden items](MenuItem.md#attr-menuitemhidden), use [Menu.getItemNum](#method-menugetitemnum) instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem) | false | — | Menu Item to find |

### Returns

`[int](../main.md#type-int)` — index of the item in the visible items, or -1 if not found.

### Groups

- menuItems

### See Also

- [Menu.filterHiddenItems](#attr-menufilterhiddenitems)

---
## Method: Menu.setItemHidden

### Description
Hides or shows the menu item according to the value of newState, and redraws the menu if necessary. Returns true if there's a change in the hidden state.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[number](#type-number) | false | — | MenuItem in question, or its index. Note that if an index is passed it will be interpreted as the index in the full specified set of items rather than the visible-index of the item. |
| newState | [boolean](../main.md#type-boolean) | true | — | true to hide the menu item, false to show it. |

### Returns

`[boolean](../main.md#type-boolean)` — true if the hidden state was changed

### See Also

- [Menu.filterHiddenItems](#attr-menufilterhiddenitems)

---
## Method: Menu.setItemProperties

### Description
Set arbitrary properties for a particular menu item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[int](../main.md#type-int) | false | — | MenuItem or visible index of the MenuItem |
| properties | [MenuItem Properties](#type-menuitem-properties) | false | — | properties to apply to the item |

---
## Method: Menu.setShowIcons

### Description
Show or hide the checkmark/custom icon column at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showIcons | [boolean](../main.md#type-boolean) | false | — | whether the icon column should be displayed |

---
## Method: Menu.getSubmenu

### Description
Get the submenu for a particular menu item.

Override to provide dynamic generation of submenus.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[int](../main.md#type-int) | false | — | MenuItem or visible index of the MenuItem |

### Returns

`[Menu](#type-menu)` — the submenu

**Flags**: A

---
## Method: Menu.getItemNum

### Description
Given a MenuItem, return its index in the [full set of items](#method-menugetallitems), including [hidden items](MenuItem.md#attr-menuitemhidden).

To retrieve the item's position in the currently visible set of items, use [Menu.getVisibleItemNum](#method-menugetvisibleitemnum).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem) | false | — | Menu Item to find |

### Returns

`[int](../main.md#type-int)` — index of the item, or -1 if not defined.

### Groups

- menuItems

---
## Method: Menu.setCriteria

### Description
This DataBoundComponent method is not supported - use [initialCriteria](#attr-menuinitialcriteria) to apply criteria to the fetches made by menus.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../main_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria) | false | — | new criteria to show |

---
## Method: Menu.setItemIcon

### Description
Sets the icon and disabled icon (if specified) for a particular menu item and redraws the menu if necessary. Returns true if the icon changed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[int](../main.md#type-int) | false | — | MenuItem or visible index of the MenuItem |
| newIcon | [String](#type-string) | false | — | new icon URL |
| newDisabledIcon | [String](#type-string) | true | — | new icon URL for disabled image |

### Returns

`[boolean](../main.md#type-boolean)` — true == something changed, redraw is called for

---
## Method: Menu.getData

### Description
Get the visible MenuItems in the current menu.

Note that if [Menu.filterHiddenItems](#attr-menufilterhiddenitems) is true, and any items are marked as [MenuItem.hidden](MenuItem.md#attr-menuitemhidden) or have [visibleWhen rules](MenuItem.md#attr-menuitemvisiblewhen), this method will return a [FilteredList](FilteredList.md#class-filteredlist) with criteria set to exclude any hidden items

To retrieve the full set of items, including hidden items, use [Menu.getAllItems](#method-menugetallitems).

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — —

---
## Method: Menu.setItemTitle

### Description
Sets the title of a particular menu item to the string specified by newTitle and redraws the menu if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[int](../main.md#type-int) | false | — | MenuItem or visible index of the MenuItem |
| newTitle | [String](#type-string) | false | — | new title |

### Returns

`[boolean](../main.md#type-boolean)` — true if the title was changed, and false otherwise

---
## Method: Menu.itemClick

### Description
Executed when a menu item with no click handler is clicked by the user. This itemClick handler must be specified as a function. It is passed an item parameter that is a reference to the clicked menu item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Object](../main.md#type-object) | false | — | pointer to the item in question |
| colNum | [number](#type-number) | true | — | Index of the column clicked by the user. May be null if this menu item was activated in response to a keyboard event. |

### Returns

`[boolean](../main.md#type-boolean)` — false if event processing should be stopped, true to continue

**Flags**: A

---
## Method: Menu.getAllItems

### Description
Retrieves the full set of items for this menu, including [hidden items](MenuItem.md#attr-menuitemhidden)

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — —

---
## Method: Menu.showSubmenu

### Description
Show the submenu for the specified item, if it has one.

Normally triggered automatically by user interaction.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[number](#type-number) | false | — | the item in question, or its index |

### Groups

- visibility

**Flags**: A

---
## Method: Menu.setData

### Description
Change the set of items to display in this menu. Note that if [Menu.filterHiddenItems](#attr-menufilterhiddenitems) is true and any items are [hidden](MenuItem.md#attr-menuitemhidden), data supplied as an Array will be converted to a [FilteredList](FilteredList.md#class-filteredlist) in order to filter out hidden items. To get the full specified data set as an array, including hidden items, use [Menu.getAllItems](#method-menugetallitems).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| items | [Array of MenuItem](#type-array-of-menuitem)|[Array of Record[]](#type-array-of-record)|[Tree](#type-tree)|[RecordList](#type-recordlist) | false | — | new items for this menu |

### Groups

- data

---
## Method: Menu.getCellStyle

### Description
Return the CSS class for a cell. By default this method has the following implementation:  
\- return any custom style for the record ([GridRenderer.recordCustomStyleProperty](GridRenderer.md#attr-gridrendererrecordcustomstyleproperty)) if defined.  
\- create a style name based on the result of [GridRenderer.getBaseStyle](GridRenderer.md#method-gridrenderergetbasestyle) and the state of the record using the rules described in [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes).

Cell Styles are customizable by:

*   attaching a custom style to a record by setting `record[this.recordCustomStyleProperty]` to some valid CSS style name.
*   modifying the base style returned by getBaseStyle() \[see that method for further documentation on this\]
*   overriding this function

In addition to this, [getCellCSSText()](GridRenderer.md#method-gridrenderergetcellcsstext) may be overriden to provide custom cssText to apply on top of the styling attributes derived from the named style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object for this row and column |
| rowNum | [number](#type-number) | false | — | number of the row |
| colNum | [number](#type-number) | false | — | number of the column |

### Returns

`[CSSStyleName](../main.md#type-cssstylename)` — CSS style for this cell

### Groups

- appearance

---
## Method: Menu.getItem

### Description
Get a particular MenuItem by index. Note that by default the index passed in is interpreted as the position within currently visible set of items for the menu, not including hidden items.

To look up an item based on its position in the full set of [specified items](#method-menugetallitems), including those that are not visible, pass in the `logicalIndex` parameter.

If passed a MenuItem, returns it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [int](../main.md#type-int) | false | — | index of the MenuItem |
| logicalIndex | [boolean](../main.md#type-boolean) | true | — | Interpret the index passed in with regards to the full set of specified items. |

### Returns

`[MenuItem](#type-menuitem)` — the MenuItem, Pointer to the item, or null if not defined

### Groups

- menuItems

---
## Method: Menu.setItems

### Description
Synonym for [Menu.setData](#method-menusetdata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| items | [Array of MenuItem](#type-array-of-menuitem) | false | — | new items for this menu |

### Groups

- data

---
## Method: Menu.getItems

### Description
Synonym for menu.getData()

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — —

---
## Method: Menu.setItemChecked

### Description
Checks or unchecks the menu item according to the value of newState, and redraws the menu if necessary. Returns true if there's a change in the checked state.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [MenuItem](#type-menuitem)|[int](../main.md#type-int) | false | — | MenuItem or visible index of the MenuItem |
| newState | [boolean](../main.md#type-boolean) | true | — | true to check the menu item, false to uncheck it. If not passed, true is assumed |

### Returns

`[boolean](../main.md#type-boolean)` — true if the checked state was changed

---
## Method: Menu.hideContextMenu

### Description
Hide the context menu - alias for hide()

### Groups

- visibility

---
## Method: Menu.showContextMenu

### Description
Show this menu as a context menu, that is, immediately adjacent to the current mouse position.

### Returns

`[Boolean](#type-boolean)` — false == stop processing this event

### Groups

- visibility

---
## Method: Menu.setShowSubmenus

### Description
Show or hide the submenu indicator column at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showSubmenus | [boolean](../main.md#type-boolean) | false | — | whether the submenu indicator column should be displayed |

---
## Method: Menu.fetchData

### Description
This DataBoundComponent method does not apply to Menu.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../main_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../main_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

---
