# Toolbar Documentation

[← Back to API Index](../main.md)

---

## Class: Toolbar

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A Toolbar creates a vertical or horizontal strip of similar components (typically Buttons) and provides managed resizing and reordering behavior over those components.

If you are creating a bar with a mixture of different elements (eg some MenuButtons, some Labels, some Buttons, some custom components), you want to use a [ToolStrip](ToolStrip.md#class-toolstrip). A Toolbar is better suited for managing a set of highly similar, interchangeable components, such as ListGrid headers.

---
## Attr: Toolbar.canReorderItems

### Description
If true, items can be reordered by dragging on them.

### Groups

- dragndrop

**Flags**: IRWA

---
## Attr: Toolbar.buttons

### Description
An array of button object initializers. See the Button Widget Class for standard button properties. The following additional properties can also be specified for button sizing and positioning on the toolbar itself:  
  

*   width--Specifies the width of this button as an absolute number of pixels, a named property of the toolbar that specifies an absolute number of pixels, a percentage of the remaining space (e.g. '60%'), or "\*" (default) to allocate an equal portion of the remaining space.
*   height--Specifies the height of this button.
*   extraSpace--Specifies an optional amount of extra space, in pixels, to separate this button from the next button in the toolbar.

### See Also

- [Toolbar.addButtons](#method-toolbaraddbuttons)
- [Toolbar.removeButtons](#method-toolbarremovebuttons)
- [Button](Button.md#class-button)

**Flags**: IRW

---
## Attr: Toolbar.buttonDefaults

### Description
Settings to apply to all buttons of a toolbar. Properties that can be applied to button objects can be applied to all buttons of a toolbar by specifying them in buttonDefaults using the following syntax:  
`buttonDefaults:{property1:value1, property2:value2, ...}`  
See the Button Widget Class for standard button properties.

### Groups

- appearance

### See Also

- [Button](Button.md#class-button)

**Flags**: IRWA

---
## Attr: Toolbar.buttonConstructor

### Description
Default constructor for toolbar items.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: Toolbar.canAcceptDrop

### Description
If true, items (buttons) can be dropped into this toolbar, and the toolbar will show a drop line at the drop location. Override drop() to decide what happens when the item is dropped.

### Groups

- dragndrop

**Flags**: IRWA

---
## Attr: Toolbar.createButtonsOnInit

### Description
If set to true, causes child buttons to be created during initialization, instead of waiting until draw().

This property principally exists for backwards compatibility; the default behavior of waiting until draw makes certain pre-draw operations more efficient (such as adding, removing or reordering buttons). However, if you have code that assumes Buttons are created early and crashes if they are not, `createButtonsOnInit` will allow that code to continue working, with a minor performance penalty.

**Flags**: IR

---
## Attr: Toolbar.vertical

### Description
Indicates whether the buttons are drawn horizontally from left to right (false), or vertically from top to bottom (true).

### Groups

- appearance

**Flags**: IRW

---
## Attr: Toolbar.canResizeItems

### Description
If true, items (buttons) can be resized by dragging on them.

### Groups

- dragndrop

**Flags**: IRWA

---
## Method: Toolbar.itemDragResized

### Description
Observable, overrideable method - called when one of the Toolbar buttons is drag resized.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemNum | [number](#type-number) | false | — | the index of the item that was resized |
| newSize | [number](#type-number) | false | — | the new size of the item |

---
## Method: Toolbar.getButton

### Description
Retrieves a button widget instance (within this toolbar) from the name / ID / index / descriptor object for the button (as with the getButtonNumber() method) This provides a way to access a toolbar button's properties and methods directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [number](#type-number)|[String](#type-string)|[Object](../main.md#type-object) | false | — | identifier for the button to retrieve |

### Returns

`[Button](#type-button)` — the button, or null if the button wasn't found

### Groups

- buttons

### See Also

- [Toolbar.getButtonNumber](#method-toolbargetbuttonnumber)

---
## Method: Toolbar.deselectButton

### Description
Deselects the specified button from the toolbar, where buttonID is the index of the button's object initializer. The button will be redrawn if necessary. The button identifier can be a number (index), string (id), or object (widget or init block), as with the getButtonNumber() method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buttonID | [number](#type-number)|[String](#type-string)|[Object](../main.md#type-object)|[Canvas](#type-canvas) | false | — | Button / Button identifier |

### Groups

- selection

### See Also

- [Toolbar.getButtonNumber](#method-toolbargetbuttonnumber)

---
## Method: Toolbar.setCanResizeItems

### Description
Setter for updating [Toolbar.canResizeItems](#attr-toolbarcanresizeitems) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canResizeItems | [boolean](../main.md#type-boolean) | false | — | New value for this.canResizeItems |

---
## Method: Toolbar.addButtons

### Description
Add a list of buttons to the toolbar

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buttons | [Array of Object](#type-array-of-object) | true | — | list of button object initializers. |
| position | [number](#type-number) | true | — | position to add the new buttons at |

---
## Method: Toolbar.itemDoubleClick

### Description
Called when one of the buttons receives a double-click event

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Button](#type-button) | false | — | pointer to the button in question |
| itemNum | [number](#type-number) | false | — | number of the button in question |

### Groups

- event handling

**Flags**: A

---
## Method: Toolbar.itemClick

### Description
Called when one of the buttons receives a click event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [StatefulCanvas](#type-statefulcanvas) | false | — | button in question |
| itemNum | [number](#type-number) | false | — | number of the button in question |

### Groups

- event handling

**Flags**: A

---
## Method: Toolbar.removeButtons

### Description
Remove a list of buttons from the toolbar

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buttons | [Array](#type-array) | true | — | Array of buttons to remove. Buttons may be specified as pointers to the button instances contained in this toolbar, or numbers indicating the index of the buttons in `this.buttons`. |

---
## Method: Toolbar.getButtonNumber

### Description
get the index of a button in the buttons array

The button can be specified as -

*   an index within this.buttons (just returned)
*   the ID property of a button
*   a pointer to the button descriptor object in this.buttons
*   the actual button widget in this.members

returns -1 if not found

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| button | [number](#type-number)|[String](#type-string)|[Button Object](#type-button-object)|[Button Widget](#type-button-widget) | false | — | — |

### Returns

`[number](#type-number)` — index of the button in question

**Flags**: A

---
## Method: Toolbar.setButtons

### Description
Apply a new set of buttons to render in this toolbar as [Toolbar.buttons](#attr-toolbarbuttons).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newButtons | [Array of Button Properties](#type-array-of-button-properties) | true | — | properties to create each button from |

---
## Method: Toolbar.selectButton

### Description
Given an identifier for a button, select it. The button identifier can be a number (index), string (id), or object (widget or init block), as with the getButtonNumber() method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buttonID | [number](#type-number)|[String](#type-string)|[Object](../main.md#type-object)|[Canvas](#type-canvas) | false | — | Button / Button identifier |

### Groups

- selection

### See Also

- [Toolbar.getButtonNumber](#method-toolbargetbuttonnumber)

---
