# MenuButton Documentation

[← Back to API Index](../main.md)

---

## Class: MenuButton

*Inherits from:* [Button](Button.md#class-button)

### Description
Simple subclass of button associated with a menu widget (gets shown below the button).

---
## Attr: MenuButton.title

### Description
Default title for the button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: MenuButton.menu

### Description
The menu to show.

For a menu button with no menu (menu: null) the up/down arrow image can be suppressed by setting [showMenuButtonImage](#attr-menubuttonshowmenubuttonimage): `false`.

### Groups

- menu

**Flags**: IRW

---
## Attr: MenuButton.menuButtonImage

### Description
Image for menu button indicating that the button expands a menu. This image is shown for menus expanding down from the button. Menu direction is controlled by [MenuButton.showMenuBelow](#attr-menubuttonshowmenubelow).

### Groups

- menu

### See Also

- [MenuButton.menuButtonImageUp](#attr-menubuttonmenubuttonimageup)

**Flags**: IRA

---
## Attr: MenuButton.rollOverMenuHideDelay

### Description
When [showMenuOnRollOver](#attr-menubuttonshowmenuonrollover) is true, this is the delay in milliseconds before the menu is automatically hidden following mouseOut.

### Groups

- menu

**Flags**: IR

---
## Attr: MenuButton.menuAnimationEffect

### Description
Allows you to specify an animation effect to apply to the menu when it is being shown. Valid options are "none" (no animation), "fade", "slide" and "wipe". If unspecified falls through to `menu.showAnimationEffect`

**Flags**: IRWA

---
## Attr: MenuButton.autoDestroyMenu

### Description
If this menuButton is [destroyed](Canvas.md#method-canvasdestroy), should it also destroy its [MenuButton.menu](#attr-menubuttonmenu)?

### Groups

- menu

**Flags**: IRW

---
## Attr: MenuButton.showMenuButtonImage

### Description
Show menu button image (up / down arrowhead) for this menu button.

### Groups

- menu

**Flags**: IR

---
## Attr: MenuButton.icon

### Description
This property corresponds to the inherited [Button.icon](Button.md#attr-buttonicon) property, which is used to display the menuButtonImage, so anything you attempt to set there would be clobbered by the internal usage.

You could add an icon via the [MenuButton.title](#attr-menubuttontitle) property, by using [Canvas.imgHTML](Canvas.md#method-canvasimghtml) to generate an appropriate `<img>` tag and pre-pending it to your title.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: MenuButton.menuButtonImageUp

### Description
Image for menu button indicating that the button expands a menu. This image is shown for menus expanding up from the button. Menu direction is controlled by [MenuButton.showMenuBelow](#attr-menubuttonshowmenubelow).

### Groups

- menu

### See Also

- [MenuButton.menuButtonImage](#attr-menubuttonmenubuttonimage)

**Flags**: IRA

---
## Attr: MenuButton.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: MenuButton.hiliteAccessKey

### Description
If this MenuButton has a specified [accessKey](Canvas.md#attr-canvasaccesskey), underline it in the title of the button by default

**Flags**: IR

---
## Attr: MenuButton.height

### Description
Default height of the button.

**Flags**: IRW

---
## Attr: MenuButton.showMenuOnRollOver

### Description
Should the menu be shown automatically when the mouse moves over the button?

When enabled, menus used with this `MenuButton` should not be used with any other component.

### Groups

- menu

**Flags**: IR

---
## Attr: MenuButton.showMenuBelow

### Description
The menu drops down below the menu button. Set to false if the menu should appear above the menu button.

Note that this setting may be ignored if it would cause the menu to be clipped by the browser viewport.

### Groups

- menu

**Flags**: IRW

---
## Attr: MenuButton.menuAlign

### Description
The horizontal alignment of this button's menu, in relation to the button. When unset, default behavior is to align the right edges of button and menu if the page is in RTL mode, and the left edges otherwise.

### Groups

- menu

**Flags**: IR

---
## Method: MenuButton.setShowMenuBelow

### Description
Setter for the 'showMenuButtonBelow' property - determines whether the menu will be shown above or below the `MenuButton`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| below | [boolean](../main.md#type-boolean) | false | — | True if the menu should be shown below the `MenuButton`. |

### Groups

- menu

---
## Method: MenuButton.setShowMenuButtonImage

### Description
Setter for the 'showMenuButtonImage' property - shows/hides the menu button image at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../main.md#type-boolean) | false | — | Should the image be shown |

### Groups

- menu

---
## Method: MenuButton.showMenu

### Description
Programmatically forces this MenuButton to show it's menu.

---
