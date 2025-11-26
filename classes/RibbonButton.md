# RibbonButton Documentation

[← Back to API Index](../reference.md)

---

## Class: RibbonButton

*Inherits from:* [Button](Button.md#class-button)

### Description
A Button subclass that displays an [icon](#attr-ribbonbuttonicon), [title](#attr-ribbonbuttonshowbuttontitle) and optional [menuIcon](#attr-ribbonbuttonmenuiconsrc) and is capable of [horizontal and vertical](#attr-ribbonbuttonvertical) orientation.

---
## Attr: RibbonButton.showTitle

### Description
showTitle is not applicable to this class - use [RibbonButton.showButtonTitle](#attr-ribbonbuttonshowbuttontitle) instead.

**Flags**: IRW

---
## Attr: RibbonButton.menuAlign

### Description
The horizontal alignment of this button's menu, in relation to the button. When unset, default behavior is to align the right edges of button and menu if the page is in RTL mode, and the left edges otherwise.

### Groups

- menu

**Flags**: IR

---
## Attr: RibbonButton.menuIconHeight

### Description
The height of the icon for this button.

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.iconOrientation

### Description
This attribute is not supported in this subclass. However, RTL mode is still supported.

**Flags**: IRW

---
## Attr: RibbonButton.icon

### Description
Icon to show to the left of or above the title, according to the button's [orientation](#attr-ribbonbuttonvertical).

When specifying `vertical = true`, this icon will be stretched to the [RibbonButton.largeIconSize](#attr-ribbonbuttonlargeiconsize) unless a [RibbonButton.largeIcon](#attr-ribbonbuttonlargeicon) is specified.

### Groups

- icon

**Flags**: IRW

---
## Attr: RibbonButton.baseStyle

### Description
Default stateful CSS class for this button. When [RibbonButton.iconStyle](#attr-ribbonbuttoniconstyle) or [RibbonButton.menuIconStyle](#attr-ribbonbuttonmenuiconstyle) are unset, they will default to the value of this attribute, suffixed with `H/VIcon` or `H/VMenuIcon` respectively, depending on the value of [RibbonButton.vertical](#attr-ribbonbuttonvertical).

### Groups

- appearance

**Flags**: IRW

---
## Attr: RibbonButton.menu

### Description
The menu to show when the [menu-icon](#attr-ribbonbuttonmenuiconsrc) is clicked.

For a menu button with no menu (menu: null) the up/down arrow image can be suppressed by setting [showMenuIcon](#attr-ribbonbuttonshowmenuicon): `false`.

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.showMenuIconDown

### Description
Whether to show a Down version of the [menuIcon](#attr-ribbonbuttonmenuiconsrc).

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.iconStyle

### Description
Default CSS class for this button's [RibbonButton.icon](#attr-ribbonbuttonicon). If unset, defaults to [RibbonButton.baseStyle](#attr-ribbonbuttonbasestyle) suffixed with `VIcon` or `HIcon` depending on the value of [RibbonButton.vertical](#attr-ribbonbuttonvertical).

### Groups

- appearance

**Flags**: IRW

---
## Attr: RibbonButton.rowSpan

### Description
When used in a [RibbonBar](RibbonBar.md#class-ribbonbar), the number of rows this button should occupy in a single [column](RibbonGroup.md#attr-ribbongroupcolumnlayout).

### Groups

- layout

**Flags**: IRW

---
## Attr: RibbonButton.largeIconSize

### Description
The size of the large icon for this button. If [RibbonButton.largeIcon](#attr-ribbonbuttonlargeicon) is not specified, the [normal icon](#attr-ribbonbuttonicon) will be stretched to this size.

### Groups

- icon

**Flags**: IRW

---
## Attr: RibbonButton.menuIconSrc

### Description
Base URL for an Image that shows a [menu](Menu.md#class-menu) when clicked. See also [RibbonButton.showMenuIconDisabled](#attr-ribbonbuttonshowmenuicondisabled) and [RibbonButton.showMenuIconOver](#attr-ribbonbuttonshowmenuiconover).

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.menuIconWidth

### Description
The width of the icon for this button.

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.showButtonTitle

### Description
Whether to show the title-text for this RibbonButton. If set to false, title-text is omitted altogether and just the icon is displayed.

### Groups

- button

**Flags**: IRW

---
## Attr: RibbonButton.menuAnimationEffect

### Description
Allows you to specify an animation effect to apply to the menu when it is being shown. Valid options are "none" (no animation), "fade", "slide" and "wipe". If unspecified falls through to `menu.showAnimationEffect`

### Groups

- menu

**Flags**: IRWA

---
## Attr: RibbonButton.vertical

### Description
Whether this button renders vertically. Renders the [icon](#attr-ribbonbuttonicon), [title](#attr-ribbonbuttonshowbuttontitle) and potentially [menuIcon](#attr-ribbonbuttonmenuiconsrc) from top to bottom, when true, and from left to right when false.

### Groups

- layout

**Flags**: IRW

---
## Attr: RibbonButton.showMenuIcon

### Description
Whether to show the [menu-icon](#attr-ribbonbuttonmenuiconsrc) which fires the [RibbonButton.menuIconClick](#method-ribbonbuttonmenuiconclick) notification method when clicked.

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.align

### Description
Horizontal alignment of this button's content. If unset, [vertical buttons](#attr-ribbonbuttonvertical) are center-aligned and horizontal buttons left-aligned by default.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RibbonButton.orientation

### Description
The orientation of this RibbonButton. The default value, "vertical", renders [icon](#attr-ribbonbuttonicon), [title](#attr-ribbonbuttonshowbuttontitle) and potentially [menuIcon](#attr-ribbonbuttonmenuiconsrc), from top to bottom: "horizontal" does the same from top to bottom.

### Groups

- layout

**Deprecated**

**Flags**: IRW

---
## Attr: RibbonButton.showIcon

### Description
Whether to show an Icon in this RibbonButton. Set to false to render a text-only button.

### Groups

- icon

**Flags**: IRW

---
## Attr: RibbonButton.iconAlign

### Description
This attribute is not supported in this subclass. However, RTL mode is still supported.

**Flags**: IRW

---
## Attr: RibbonButton.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: RibbonButton.showMenuIconDisabled

### Description
Whether to show a Disabled version of the [menuIcon](#attr-ribbonbuttonmenuiconsrc).

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.largeIcon

### Description
Icon to show above the title when [Orientation](../reference_2.md#type-orientation) is "vertical".

If a largeIcon is not specified, the [normal icon](#attr-ribbonbuttonicon) will be stretched to the [RibbonButton.largeIconSize](#attr-ribbonbuttonlargeiconsize).

### Groups

- icon

**Flags**: IRW

---
## Attr: RibbonButton.valign

### Description
Vertical alignment of this button's content. If unset, [vertical buttons](#attr-ribbonbuttonvertical) are top-aligned and horizontal buttons center-aligned by default.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RibbonButton.menuIconStyle

### Description
Default CSS class to apply to the element showing this button's [menu-icon](#attr-ribbonbuttonmenuiconsrc). If unset, defaults to [RibbonButton.baseStyle](#attr-ribbonbuttonbasestyle) suffixed with `VMenuIcon` or `HMenuIcon` depending on the value of [RibbonButton.vertical](#attr-ribbonbuttonvertical).

### Groups

- appearance

**Flags**: IRW

---
## Attr: RibbonButton.showMenuBelow

### Description
The menu drops down below the menu button. Set to false if the menu should appear above the menu button.

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.showMenuOnClick

### Description
If set to true, shows this button's [menu](Menu.md#class-menu) when a user clicks anywhere in the button, rather than specifically on the [menuIcon](#attr-ribbonbuttonmenuiconsrc).

Note that this property has a different meaning than [showMenuOnClick](StatefulCanvas.md#attr-statefulcanvasshowmenuonclick) in the ancestor class [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas).

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.showMenuIconOver

### Description
Whether to show an Over version of the [menuIcon](#attr-ribbonbuttonmenuiconsrc).

### Groups

- menu

**Flags**: IRW

---
## Attr: RibbonButton.iconSize

### Description
The size of the normal icon for this button.

### Groups

- icon

**Flags**: IRW

---
## Method: RibbonButton.getIcon

### Description
Returns the URL for the current icon.

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — URL of current icon

### Groups

- icon

---
## Method: RibbonButton.setMenu

### Description
The menu to show when the [menu-icon](#attr-ribbonbuttonmenuiconsrc) is clicked.

For a menu button with no menu (menu: null) the up/down arrow image can be suppressed by setting [showMenuIcon](#attr-ribbonbuttonshowmenuicon): `false`. Note that `showMenuIcon` is updated automatically by calls to [RibbonButton.setMenu](#method-ribbonbuttonsetmenu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| menu | [Menu](#type-menu) | false | — | a menu to assign to this button |

### Groups

- menu

---
## Method: RibbonButton.iconClick

### Description
Notification method fired when a user clicks on the [icon](#attr-ribbonbuttonicon) in this RibbonButton. Return false to suppress the standard click handling code.

### Returns

`[Boolean](#type-boolean)` — return false to cancel event-bubbling

---
## Method: RibbonButton.setIcon

### Description
Sets a new Icon for this button after initialization.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [SCImgURL](../reference.md#type-scimgurl) | false | — | URL of new icon |

### Groups

- icon

---
## Method: RibbonButton.showMenu

### Description
Shows this button's [RibbonButton.menu](#attr-ribbonbuttonmenu). Called automatically when a user clicks the [menuIcon](#attr-ribbonbuttonmenuiconsrc).

### Returns

`[Boolean](#type-boolean)` — true if a menu was shown

### Groups

- menu

---
## Method: RibbonButton.setLargeIcon

### Description
Sets a new Large-Icon for vertical buttons after initialization - synonymous with [setIcon](#method-ribbonbuttonseticon) for normal horizontal buttons.

### Groups

- icon

---
## Method: RibbonButton.menuIconClick

### Description
Notification method fired when a user clicks on the menuIcon on this RibbonButton. Return false to suppress the standard click handling code.

### Returns

`[Boolean](#type-boolean)` — return false to cancel event-bubbling

---
## Method: RibbonButton.click

### Description
Notification method fired when a user clicks anywhere on this button. If the click occurred directly on the [icon](Button.md#attr-buttonicon) or the [menuIcon](#attr-ribbonbuttonmenuiconsrc), the related notifications [iconClick](#method-ribbonbuttoniconclick) and [menuIconClick](#method-ribbonbuttonmenuiconclick) are fired first and must return false to prevent this notification from firing.

If a [menu](Menu.md#class-menu) is installed then, by default, it is only displayed when a user clicks on the [menuIcon](#attr-ribbonbuttonmenuiconsrc). This can be altered via [showMenuOnClick](#attr-ribbonbuttonshowmenuonclick).

### Returns

`[Boolean](#type-boolean)` — return false to cancel event-bubbling

---
