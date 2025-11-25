# MenuBar Documentation

[← Back to API Index](../main.md)

---

## Class: MenuBar

*Inherits from:* [Toolbar](Toolbar.md#class-toolbar)

### Description
A MenuBar is a bar of buttons used to show a set of menus.

---
## Attr: MenuBar.menus

### Description
An array of menu object initializers or instantiated menu objects. Buttons for each menu item will automatically be created. See the Menu Widget Class for fundamental menu properties and other properties. Titles for the buttons are derived from the `title` property of each menu.

### See Also

- [Menu](Menu.md#class-menu)

**Flags**: IRW

---
## Attr: MenuBar.tabIndex

### Description
By default exclude menubars from the page's tab order. To include a menubar in the page's tab order, set tabIndex to an explicit tab index, or `null` for automatically assigned tabIndex

**Flags**: IRWA

---
## Attr: MenuBar.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Method: MenuBar.removeMenus

### Description
Dynamically remove menus from the menuBar. Will update the visible set of buttons as appropriate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| menus | [Array](#type-array) | false | — | Array of menus to remove (will accept actual Menu components, or numbers representing the index of the menus in the current menus array) |

---
## Method: MenuBar.showMenu

### Description
Shows (opens) a menu.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| menu | [Menu](#type-menu)|[Integer](../main_2.md#type-integer) | false | — | menu to show (may be specified as a menu object, or index of the menu from [this.menus](#attr-menubarmenus)). |

---
## Method: MenuBar.addMenus

### Description
Dynamically update the menuBar to include additional menus. Will update the visible set of buttons as appropriate

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMenus | [Array](#type-array) | false | — | Array of new menus to add |
| position | [number](#type-number) | false | — | desired starting position of the new menus in the existing menus array |

---
## Method: MenuBar.setMenus

### Description
Dynamically reset the set of menus displayed by this menu bar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| menus | [Array of Menu](#type-array-of-menu) | false | — | array of new menus for this menubar |

---
## Method: MenuBar.setButtons

### Description
Invalid to call on Menubar, use [MenuBar.setMenus](#method-menubarsetmenus) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newButtons | [Array of Button Properties](#type-array-of-button-properties) | true | — | invalid; do not call |

---
