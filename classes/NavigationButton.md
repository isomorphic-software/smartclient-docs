# NavigationButton Documentation

[← Back to API Index](../main.md)

---

## Class: NavigationButton

*Inherits from:* [Button](Button.md#class-button)

### Description
Specially styled Button subclass used by the [NavigationBar](NavigationBar.md#class-navigationbar) class.

---
## Attr: NavigationButton.direction

### Description
Navigation direction for this button. If set to `"forward"` or `"back"` the special [NavigationButton.forwardBaseStyle](#attr-navigationbuttonforwardbasestyle) or [NavigationButton.backBaseStyle](#attr-navigationbuttonbackbasestyle) will be applied.

**Flags**: IRW

---
## Attr: NavigationButton.forwardBaseStyle

### Description
Base style for navigation buttons where [Direction](../main_2.md#type-direction) is set to `"forward"`

**Flags**: IRW

---
## Attr: NavigationButton.backBaseStyle

### Description
Base style for navigation buttons where [Direction](../main_2.md#type-direction) is set to `"back"`

**Flags**: IRW

---
## Attr: NavigationButton.baseStyle

### Description
Default baseStyle for navigation buttons. Note that the special [NavigationButton.backBaseStyle](#attr-navigationbuttonbackbasestyle) and [NavigationButton.forwardBaseStyle](#attr-navigationbuttonforwardbasestyle) are applied if [NavigationButton.direction](#attr-navigationbuttondirection) is set.

**Flags**: IRW

---
