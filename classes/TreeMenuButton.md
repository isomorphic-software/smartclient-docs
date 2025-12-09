# TreeMenuButton Documentation

[← Back to API Index](../reference.md)

---

## Class: TreeMenuButton

*Inherits from:* [MenuButton](MenuButton.md#class-menubutton)

### Description
Button used to display a hierarchical Menu group for representing / selecting tree data.

_**Important Note:** this class should not be used directly - it is exposed purely for [i18n reasons.](../kb_topics/i18nMessages.md#kb-topic-i18n-messages)_

### See Also

- [SelectionTreeMenu](../reference.md#class-selectiontreemenu)

---
## Attr: TreeMenuButton.title

### Description
Title for this button. If not specified, the selected value from the tree will be displayed instead.

**Flags**: IRW

---
## Attr: TreeMenuButton.treeMenu

### Description
AutoChild menu displayed when the button is clicked.

**Flags**: IR

---
## Attr: TreeMenuButton.selectedBaseStyle

### Description
Base style to apply to the selected path within the menu. (The "over" version of this style should also be defined in the stylesheet applied to this widget).

**Flags**: IRW

---
## Attr: TreeMenuButton.treeMenuConstructor

### Description
Widget class for the menu created by this button. The default is [SelectionTreeMenu](../reference.md#class-selectiontreemenu).

**Flags**: IR

---
## Attr: TreeMenuButton.dataProperties

### Description
For a `TreeMenuButton` that uses a DataSource, these properties will be passed to the automatically-created ResultTree. This can be used for various customizations such as modifying the automatically-chosen [Tree.parentIdField](Tree.md#attr-treeparentidfield).

### Groups

- databinding

**Flags**: IR

---
## Attr: TreeMenuButton.emptyMenuMessage

### Description
If this button's menu (or any of its submenus) are empty, this property can be used to specify the message to display (as a disabled item) in the empty menu.

**Flags**: IRW

---
## Attr: TreeMenuButton.showPath

### Description
If [title](#attr-treemenubuttontitle) is null, when the user selects an item, should we show the full path to the item, or just the item's title as the button's title?

**Flags**: IRW

---
## Attr: TreeMenuButton.pathSeparatorString

### Description
If [showPath](#attr-treemenubuttonshowpath) is true, this property specifies what will appear between the folders in the selected value's path.

**Flags**: IRW

---
## Attr: TreeMenuButton.unselectedTitle

### Description
If [title](#attr-treemenubuttontitle) is null, this value will be displayed as a title when the user has not selected any value from the hierachichal menu.

### Groups

- i18nMessages

**Flags**: IRW

---
