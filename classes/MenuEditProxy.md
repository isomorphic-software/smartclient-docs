# MenuEditProxy Documentation

[← Back to API Index](../reference.md)

---

## Class: MenuEditProxy

*Inherits from:* [CanvasEditProxy](../reference.md#class-canvaseditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [MenuButton](MenuButton.md#class-menubutton) and [MenuBar](MenuBar.md#class-menubar) objects when editMode is enabled.

### Groups

- devTools

---
## Method: MenuEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's menu definition in wiki-style.

---
## Method: MenuEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's menu.

Lines starting with "--", "==" or "title:" are considered titles for the MenuButtons. The menuItem definitions follow the title to define the menu contents.

Each menuItem title is entered on its own line. A keyTitle can follow the title separated by a comma. A leading "x" or "o" marks the menuItem as checked. MenuItems can be marked as disabled with a leading or trailing dash (-). A sub-menu is indicated with a trailing >. Any line consisting entirely of one or more dashes (-) or equals (=) indicates a separator line.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component menu |

---
