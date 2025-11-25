# AdaptiveMenu Documentation

[← Back to API Index](../main.md)

---

## Class: AdaptiveMenu

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A menu that can either show its menu options inline, or show them via a drop-down, depending on available space in the surrounding [Layout](Layout.md#class-layout) or [ToolStrip](ToolStrip.md#class-toolstrip).

See [canAdaptWidth](Canvas.md#attr-canvascanadaptwidth) for background on adaptive layout.

---
## Attr: AdaptiveMenu.partialInlining

### Description
If there is not enough space to show the full set of items as buttons inline, how should the Adaptive menu behave?  
If `showPartialInlining` is true, the menu will render as many items as inline buttons as can be shown in the available space, plus the menu button to access the remaining items.  
If false, it will show just the menu button.

If there is enough space to show the full set of items inline they will be shown inline regardless of this property.

**Flags**: IRW

---
## Attr: AdaptiveMenu.menuButtonTitle

### Description
Title used for the [MenuButton](MenuButton.md#class-menubutton).

**Flags**: IR

---
## Attr: AdaptiveMenu.inlineImgButton

### Description
[ToolStripButton](../main.md#class-toolstripbutton) to display when [AdaptiveMenu.showIconOnlyInline](#attr-adaptivemenushowicononlyinline) is set for one [MenuItem](../main_2.md#object-menuitem)

**Flags**: R

---
## Attr: AdaptiveMenu.inlineSeparator

### Description
[ToolStripSeparator](../main.md#class-toolstripseparator) to display when [isSeparator](MenuItem.md#attr-menuitemisseparator) is set for a [MenuItem](../main_2.md#object-menuitem).

**Flags**: R

---
## Attr: AdaptiveMenu.inlineSubmenuItem

### Description
[MultiAutoChild](../main.md#type-multiautochild) used to create inline menu items for menu items that have a submenu.

The [MenuItem.icon](MenuItem.md#attr-menuitemicon) and [MenuItem.title](MenuItem.md#attr-menuitemtitle) will be rendered via [IconButton.icon](RibbonButton.md#attr-ribbonbuttonicon) and [Button.title](Button.md#attr-buttontitle) respectively; other [MenuItem](../main_2.md#object-menuitem) appearance-related properties do not apply.

**Flags**: R

---
## Attr: AdaptiveMenu.showIconOnlyInline

### Description
Default setting for [MenuItem.showIconOnlyInline](MenuItem.md#attr-menuitemshowicononlyinline). Individual items can set `showIconOnlyInline` to override this setting.

**Flags**: IR

---
## Attr: AdaptiveMenu.items

### Description
MenuItems to be show either inline or as a drop-down [Menu](Menu.md#class-menu).

When shown inline, items are rendered as different [AutoChild](../main.md#type-autochild) according to the settings on the MenuItem:

*   normal MenuItems render as the [AdaptiveMenu.inlineMenuItem](#attr-adaptivemenuinlinemenuitem), a [ToolStripButton](../main.md#class-toolstripbutton) AutoChild
*   MenuItems that have submenus render as the [AdaptiveMenu.inlineSubmenuItem](#attr-adaptivemenuinlinesubmenuitem), a [MenuButton](MenuButton.md#class-menubutton) AutoChild
*   MenuItems with [showIconOnlyInline](MenuItem.md#attr-menuitemshowicononlyinline) set render as the [AdaptiveMenu.inlineImgButton](#attr-adaptivemenuinlineimgbutton), a [ToolStripButton](../main.md#class-toolstripbutton) AutoChild
*   MenuItems where [MenuItem.embeddedComponent](MenuItem.md#attr-menuitemembeddedcomponent) has been specified will have the embedded component displayed directly instead (no AutoChild involvement here). If the the control should have different appearance when inlined vs embedded in the menu, one way to achieve this is to detect whether the parent is a Menu when it is drawn.
*   MenuItems with [isSeparator](MenuItem.md#attr-menuitemisseparator) set render as the [AdaptiveMenu.inlineSeparator](#attr-adaptivemenuinlineseparator), a [ToolStripSeparator](../main.md#class-toolstripseparator) AutoChild

**Flags**: IRW

---
## Attr: AdaptiveMenu.menuButtonIcon

### Description
Icon used for the [MenuButton](MenuButton.md#class-menubutton). Default of null means to use the default for the [MenuButton](MenuButton.md#class-menubutton) class.

**Flags**: IR

---
## Attr: AdaptiveMenu.menuButton

### Description
[MenuButton](MenuButton.md#class-menubutton) used as a drop-down control for showing any items of the menu that are not displayed inline.

**Flags**: R

---
## Attr: AdaptiveMenu.inlinePlacement

### Description
Placement of inlined items relative to the main [MenuButton](MenuButton.md#class-menubutton). Default is to place items above the menu if the parent is a Layout with [vertical orientation](Layout.md#attr-layoutorientation), otherwise to the left of the `menuButton` (or right if the [page is\\n RTL (right-to-left)](Page.md#classmethod-pageisrtl).

A setting of "center" is invalid and will cause a warning and be ignored

**Flags**: IR

---
## Attr: AdaptiveMenu.inlineMenuItem

### Description
[MultiAutoChild](../main.md#type-multiautochild) used to create inline menu items.

The [MenuItem.icon](MenuItem.md#attr-menuitemicon) and [MenuItem.title](MenuItem.md#attr-menuitemtitle) will be rendered via [Button.icon](Button.md#attr-buttonicon) and [Button.title](Button.md#attr-buttontitle) respectively; other [MenuItem](../main_2.md#object-menuitem) appearance-related properties do not apply.

**Flags**: R

---
## Attr: AdaptiveMenu.menu

### Description
Instance of the normal (non-Adaptive) [Menu](Menu.md#class-menu) class used to show items that do not fit inline.

**Flags**: IR

---
## Attr: AdaptiveMenu.showInlineSeparators

### Description
Whether [separators](../main.md#class-toolstripseparator) should be shown for inline menu items. True by default for horizontal [orientation](Layout.md#attr-layoutorientation), false for vertical.

Note, to use explicit menu separators ([MenuItem.isSeparator](MenuItem.md#attr-menuitemisseparator)) which will also show in the ToolStrip, set this property `false` to avoid showing duplicate separators in the menu.

**Flags**: IR

---
## Method: AdaptiveMenu.setItems

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| items | [Array of MenuItem](#type-array-of-menuitem)|[MenuItem](#type-menuitem) | false | — | array of items to replace current items |

---
## Method: AdaptiveMenu.setPartialInlining

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| partialInlining | [boolean](../main.md#type-boolean) | false | — | — |

---
