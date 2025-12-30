# IconMenuButton Documentation

[← Back to API Index](../reference.md)

---

## Class: IconMenuButton

*Inherits from:* [IconButton](IconButton.md#class-iconbutton)

### Description
A subclass of [IconButton](IconButton.md#class-iconbutton) that shows a menuIcon by default and implements showMenu().

This class has [showMenuIcon](IconButton.md#attr-iconbuttonshowmenuicon) set to `true` by default, and has a [IconButton.menuIconClick](IconButton.md#method-iconbuttonmenuiconclick) handler which will show the specified [IconMenuButton.menu](#attr-iconmenubuttonmenu) via a call to [IconMenuButton.showMenu](#method-iconmenubuttonshowmenu). This menuIconClick handler cancels default click behavior, so, if a user clicks the menu item, any specified [click handler](Canvas.md#method-canvasclick) for the button as a whole will not fire.

---
## Attr: IconMenuButton.showMenuBelow

### Description
The menu drops down below the menu button. Set to false if the menu should appear above the menu button.

**Flags**: IRW

---
## Attr: IconMenuButton.menuAnimationEffect

### Description
Allows you to specify an animation effect to apply to the menu when it is being shown. Valid options are "none" (no animation), "fade", "slide" and "wipe". If unspecified falls through to `menu.showAnimationEffect`

**Flags**: IRWA

---
## Attr: IconMenuButton.menu

### Description
The menu to show when the [menu-icon](IconButton.md#attr-iconbuttonmenuiconsrc) is clicked.

For a menu button with no menu (menu: null) the up/down arrow image can be suppressed by setting [showMenuButtonImage](MenuButton.md#attr-menubuttonshowmenubuttonimage): `false`.

**Flags**: IRW

---
## Attr: IconMenuButton.menuAlign

### Description
The horizontal alignment of this button's menu, in relation to the button. When unset, default behavior is to align the right edges of button and menu if the page is in RTL mode, and the left edges otherwise.

**Flags**: IR

---
## Method: IconMenuButton.showMenu

### Description
Shows this button's [IconMenuButton.menu](#attr-iconmenubuttonmenu). Called automatically when a user clicks the [menuIcon](IconButton.md#attr-iconbuttonmenuiconsrc).

### Returns

`[Boolean](#type-boolean)` — true if a menu was shown

---
