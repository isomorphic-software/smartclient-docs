# GradientEditor Documentation

[← Back to API Index](../main.md)

---

## Class: GradientEditor

*Inherits from:* [VLayout](../main.md#class-vlayout)

### Description
A widget for visually editing CSS gradients.

**Note:** this feature requires [SmartClient Enterprise](https://www.smartclient.com/product/).

---
## Attr: GradientEditor.dragSnapAngle

### Description
The angle by which drag-rotating a linear-gradient in the preview should snap. The default of 1 means a linear-gradient can be positioned to any exact degree of a circle.

**Flags**: IRW

---
## Attr: GradientEditor.showPreviewCanvas

### Description
Whether to show the [preview canvas](#attr-gradienteditorpreviewcanvas), used to display the gradient.

**Flags**: IRW

---
## Attr: GradientEditor.previewCanvas

### Description
An [AutoChild](../main.md#type-autochild) of type [Canvas](Canvas.md#class-canvas), used to display the gradient according to the defined color-stops. The canvas supports drag and click mouse interactions to update a gradient's rotation and origin.

**Flags**: R

---
## Attr: GradientEditor.gradient

### Description
The CSS gradient-statement to work with.

**Flags**: IRW

---
## Attr: GradientEditor.outputForm

### Description
A DynamicForm that shows the gradient-string produced by this editor.

**Flags**: IR

---
## Method: GradientEditor.getGradient

### Description
Returns the current state of the widget as a CSS gradient

### Returns

`[String](#type-string)` — the gradient definition

---
## Method: GradientEditor.setGradient

### Description
Parses the passed `gradient` and applies it to the UI for editing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradient | [String](#type-string) | false | — | CSS gradient string |

---
## Method: GradientEditor.gradientChanged

### Description
Notification fired whenever a user updates the gradient.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradient | [String](#type-string) | false | — | the current [gradient CSS](#attr-gradienteditorgradient) |

---
