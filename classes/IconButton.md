# IconButton Documentation

[← Back to API Index](../reference.md)

---

## Class: IconButton

*Inherits from:* [Button](Button.md#class-button)

### Description
A Button subclass that displays an [icon](#attr-iconbuttonicon), [title](#attr-iconbuttonshowbuttontitle) and optional [menuIcon](#attr-iconbuttonmenuiconsrc) and is capable of horizontal and vertical [orientation](#attr-iconbuttonorientation).

---
## Attr: IconButton.rowSpan

### Description
When used in a [RibbonBar](../reference.md#class-ribbonbar), the number of rows this button should occupy in a single [column](ToolStripGroup.md#attr-toolstripgroupcolumnlayout).

**Flags**: IRW

---
## Attr: IconButton.showMenuIconOver

### Description
Whether to show an Over version of the [menuIcon](#attr-iconbuttonmenuiconsrc).

**Flags**: IRW

---
## Attr: IconButton.valign

### Description
Vertical alignment of this button's content. If unset, [vertical buttons](#attr-iconbuttonorientation) are top-aligned and horizontal buttons center-aligned by default.

### Groups

- appearance

**Flags**: IRW

---
## Attr: IconButton.showMenuIconDown

### Description
Whether to show a Down version of the [menuIcon](#attr-iconbuttonmenuiconsrc).

**Flags**: IRW

---
## Attr: IconButton.showIcon

### Description
Whether to show an Icon in this IconButton. Set to false to render a text-only button.

**Flags**: IRW

---
## Attr: IconButton.largeIcon

### Description
Icon to show above the title when [Orientation](../reference.md#type-orientation) is "vertical".

If a largeIcon is not specified, the [normal icon](#attr-iconbuttonicon) will be stretched to the [IconButton.largeIconSize](#attr-iconbuttonlargeiconsize).

**Flags**: IRW

---
## Attr: IconButton.icon

### Description
Icon to show to the left of or above the title, according to the button's [Orientation](../reference.md#type-orientation).

When specifying `titleOrientation = "vertical"`, this icon will be stretched to the [IconButton.largeIconSize](#attr-iconbuttonlargeiconsize) unless a [IconButton.largeIcon](#attr-iconbuttonlargeicon) is specified.

**Flags**: IRW

---
## Attr: IconButton.menuIconWidth

### Description
The width of the icon for this button.

**Flags**: IRW

---
## Attr: IconButton.menuIconSrc

### Description
Base URL for an Image that shows a [menu](Menu.md#class-menu) when clicked. See also [IconButton.showMenuIconDisabled](#attr-iconbuttonshowmenuicondisabled) and [IconButton.showMenuIconOver](#attr-iconbuttonshowmenuiconover).

**Flags**: IRW

---
## Attr: IconButton.showMenuIcon

### Description
Whether to show the [menu-icon](#attr-iconbuttonmenuiconsrc) which fires the [IconButton.menuIconClick](#method-iconbuttonmenuiconclick) notification method when clicked.

**Flags**: IRW

---
## Attr: IconButton.align

### Description
Horizontal alignment of this button's content. If unset, [vertical buttons](#attr-iconbuttonorientation) are center-aligned and horizontal buttons left-aligned by default.

### Groups

- appearance

**Flags**: IRW

---
## Attr: IconButton.largeIconSize

### Description
The size of the large icon for this button. If [IconButton.largeIcon](#attr-iconbuttonlargeicon) is not specified, the [normal icon](#attr-iconbuttonicon) will be stretched to this size.

**Flags**: IRW

---
## Attr: IconButton.showButtonTitle

### Description
Whether to show the title-text for this IconButton. If set to false, title-text is omitted altogether and just the icon is displayed.

**Flags**: IRW

---
## Attr: IconButton.showMenuIconDisabled

### Description
Whether to show a Disabled version of the [menuIcon](#attr-iconbuttonmenuiconsrc).

**Flags**: IRW

---
## Attr: IconButton.orientation

### Description
The orientation of this IconButton. The default value, "horizontal", renders [icon](#attr-iconbuttonicon), [title](#attr-iconbuttonshowbuttontitle) and potentially [menuIcon](#attr-iconbuttonmenuiconsrc), from left to right: "vertical" does the same from top to bottom.

**Flags**: IRW

---
## Attr: IconButton.showMenuOnClick

### Description
If set to true, shows this button's [menu](Menu.md#class-menu) when a user clicks anywhere in the button, rather than specifically on the [menuIcon](#attr-iconbuttonmenuiconsrc).

Note that this property has a different meaning than [showMenuOnClick](StatefulCanvas.md#attr-statefulcanvasshowmenuonclick) in the ancestor class [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas).

**Flags**: IRW

---
## Attr: IconButton.baseStyle

### Description
Default CSS class for this button.

**Flags**: IRW

---
## Attr: IconButton.iconAlign

### Description
This attribute is not supported in this subclass. However, RTL mode is still supported.

**Flags**: IRW

---
## Attr: IconButton.iconSize

### Description
The size of the normal icon for this button.

**Flags**: IRW

---
## Attr: IconButton.iconOrientation

### Description
This attribute is not supported in this subclass. However, RTL mode is still supported.

**Flags**: IRW

---
## Attr: IconButton.showTitle

### Description
showTitle is not applicable to this class - use [IconButton.showButtonTitle](#attr-iconbuttonshowbuttontitle) instead.

**Flags**: IRW

---
## Attr: IconButton.menuIconHeight

### Description
The height of the icon for this button.

**Flags**: IRW

---
## Method: IconButton.click

### Description
Notification method fired when a user clicks anywhere on this button. If the click occurred directly on the [icon](Button.md#attr-buttonicon) or the [menuIcon](#attr-iconbuttonmenuiconsrc), the related notifications [iconClick](#method-iconbuttoniconclick) and [menuIconClick](#method-iconbuttonmenuiconclick) are fired first and must return false to prevent this notification from firing.

If a [menu](Menu.md#class-menu) is installed then, by default, it is only displayed when a user clicks on the [menuIcon](#attr-iconbuttonmenuiconsrc). This can be altered via [showMenuOnClick](#attr-iconbuttonshowmenuonclick).

### Returns

`[Boolean](#type-boolean)` — return false to cancel event-bubbling

---
## Method: IconButton.iconClick

### Description
Notification method fired when a user clicks on the [icon](#attr-iconbuttonicon) in this IconButton. Return false to suppress the standard click handling code.

### Returns

`[Boolean](#type-boolean)` — return false to cancel event-bubbling

---
## Method: IconButton.menuIconClick

### Description
Notification method fired when a user clicks on the menuIcon on this IconButton. Return false to suppress the standard click handling code.

### Returns

`[Boolean](#type-boolean)` — return false to cancel event-bubbling

---
## Method: IconButton.setLargeIcon

### Description
Sets a new Large-Icon for vertical buttons after initialization - synonymous with [setIcon](#method-iconbuttonseticon) for normal horizontal buttons.

---
## Method: IconButton.setIcon

### Description
Sets a new Icon for this button after initialization.

---
