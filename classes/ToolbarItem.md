# ToolbarItem Documentation

[← Back to API Index](../main.md)

---

## Class: ToolbarItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
Set of horizontally arranged buttons.

---
## Attr: ToolbarItem.colSpan

### Description
these items span all columns

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolbarItem.createButtonsOnInit

### Description
If set to true, causes the toolbar created by this item to create its child buttons during initialization, instead of waiting until draw().

See the corresponding [Toolbar attribute](Toolbar.md#attr-toolbarcreatebuttonsoninit) for more information.

**Flags**: IR

---
## Attr: ToolbarItem.buttons

### Description
List of buttons for the toolbar. Each button should be specified as a simple JS object with properties to apply to the button to be displayed. Note that any `click` stringMethod applied to the button will be passed 2 parameters: `form` and `item`.

### Groups

- items

**Flags**: IRW

---
## Attr: ToolbarItem.canvas

### Description
This item is an autoChild generated [Canvas](Canvas.md#class-canvas) displayed by the ToolbarItem and is an instance of [Toolbar](Toolbar.md#class-toolbar) by default, customizable via the [ToolbarItem.canvasConstructor](#attr-toolbaritemcanvasconstructor) attribute.

**Flags**: R

---
## Attr: ToolbarItem.buttonProperties

### Description
Default properties for this toolbar's buttons.

**Flags**: IRA

---
## Attr: ToolbarItem.endRow

### Description
these items are in a row by themselves by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolbarItem.canvasConstructor

### Description
Constructor class for this toolbarItem's [canvas](#attr-toolbaritemcanvas).

**Flags**: IRA

---
## Attr: ToolbarItem.buttonAutoFit

### Description
Default [Button.autoFit](Button.md#attr-buttonautofit) for buttons - true by default. Note that autoFit:true buttons will fit to their title regardless of specified width.

**Flags**: IRA

---
## Attr: ToolbarItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ToolbarItem.buttonBaseStyle

### Description
If specified this baseStyle will be applied to the buttons in this toolbar.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolbarItem.showTitle

### Description
Don't show a title for toolbars

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolbarItem.buttonSpace

### Description
Space between the buttons of this toolbar. Configures the [Layout.membersMargin](Layout.md#attr-layoutmembersmargin) property on the created [ToolbarItem.canvas](#attr-toolbaritemcanvas).

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolbarItem.startRow

### Description
these items are in a row by themselves by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolbarItem.vertical

### Description
Should the toolbar stack its buttons vertically or horizontally?

**Flags**: IRA

---
