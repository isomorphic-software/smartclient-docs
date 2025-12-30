# IMenuButton Documentation

[← Back to API Index](../reference.md)

---

## Class: IMenuButton

*Inherits from:* [MenuButton](MenuButton.md#class-menubutton)

### Description
IMenuButton based version of the [MenuButton](MenuButton.md#class-menubutton) class.

---
## Attr: IMenuButton.height

### Description
Default height of the button.

**Flags**: IRW

---
## Attr: IMenuButton.menu

### Description
The menu to show.

For a menu button with no menu (menu: null) the up/down arrow image can be suppressed by setting [showMenuButtonImage](MenuButton.md#attr-menubuttonshowmenubuttonimage): `false`.

**Flags**: IRW

---
## Attr: IMenuButton.autoDestroyMenu

### Description
If this menuButton is [destroyed](Canvas.md#method-canvasdestroy), should it also destroy its [MenuButton.menu](MenuButton.md#attr-menubuttonmenu)?

**Flags**: IRW

---
## Attr: IMenuButton.title

### Description
Default title for the button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: IMenuButton.menuAnimationEffect

### Description
Allows you to specify an animation effect to apply to the menu when it is being shown. Valid options are "none" (no animation), "fade", "slide" and "wipe". If unspecified falls through to `menu.showAnimationEffect`

**Flags**: IRWA

---
## Attr: IMenuButton.hiliteAccessKey

### Description
If this MenuButton has a specified [accessKey](Canvas.md#attr-canvasaccesskey), underline it in the title of the button by default

**Flags**: IR

---
## Attr: IMenuButton.menuButtonImage

### Description
Image for menu button indicating that the button expands a menu. This image is shown for menus expanding down from the button. Menu direction is controlled by [MenuButton.showMenuBelow](MenuButton.md#attr-menubuttonshowmenubelow).

### See Also

- [MenuButton.menuButtonImageUp](MenuButton.md#attr-menubuttonmenubuttonimageup)

**Flags**: IRA

---
## Attr: IMenuButton.showMenuBelow

### Description
The menu drops down below the menu button. Set to false if the menu should appear above the menu button.

**Flags**: IRW

---
## Attr: IMenuButton.showMenuButtonImage

### Description
Show menu button image (up / down arrowhead) for this menu button.

**Flags**: IR

---
## Attr: IMenuButton.menuAlign

### Description
The horizontal alignment of this button's menu, in relation to the button. When unset, default behavior is to align the right edges of button and menu if the page is in RTL mode, and the left edges otherwise.

**Flags**: IR

---
## Attr: IMenuButton.menuButtonImageUp

### Description
Image for menu button indicating that the button expands a menu. This image is shown for menus expanding up from the button. Menu direction is controlled by [MenuButton.showMenuBelow](MenuButton.md#attr-menubuttonshowmenubelow).

### See Also

- [MenuButton.menuButtonImage](MenuButton.md#attr-menubuttonmenubuttonimage)

**Flags**: IRA

---
## Method: IMenuButton.setShowMenuBelow

### Description
Setter for the 'showMenuButtonBelow' property - determines whether the menu will be shown above or below the menubutton.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| below | [boolean](../reference.md#type-boolean) | false | — | True if the menu should be shown below the menubutton. |

---
## Method: IMenuButton.setShowMenuButtonImage

### Description
Setter for the 'showMenuButtonImage' property - shows/hides the menu button image at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | Should the image be shown |

---
