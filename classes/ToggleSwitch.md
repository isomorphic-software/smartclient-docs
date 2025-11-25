# ToggleSwitch Documentation

[← Back to API Index](../main.md)

---

## Class: ToggleSwitch

*Inherits from:* [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas)

### Description
A simple control that presents a Boolean value as a toggle-switch, where the value can be toggled by clicking with the mouse, or with the Spacebar and left/right arrow-keys when [ToggleSwitch.toggleOnKeypress](#attr-toggleswitchtoggleonkeypress) is true.

---
## Attr: ToggleSwitch.defaultValue

### Description
The default value of this ToggleSwitch.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.thumbOffset

### Description
Spacing to apply inside of this ToggleSwitch, outside of the [ToggleSwitch.thumb](#attr-toggleswitchthumb).

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.thumbRadius

### Description
The CSS border-radius for the [ToggleSwitch.thumb](#attr-toggleswitchthumb). The value can be any variant of a CSS border-radius value - that is, from 1 to 4 space-separated px values, where one value affects all corners and 4 values affects individual corners. For example "10px" applies a 10px radius to all corners, where "5px 10px 15px 20px" applies a different radius to each corner, clockwise from Top-Left: "TL TR BR BL".

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.animateThumbTime

### Description
When [animateThumb](#attr-toggleswitchanimatethumb) is true, the time taken to move the [thumb](#attr-toggleswitchthumb) from one state to the other.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.thumbBaseStyle

### Description
The name of the base CSS class to apply to the [thumb](#attr-toggleswitchthumb) of this toggle switch - the actual styleName applied will be suffixed "On" or "Off", depending on this widget's current value.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.toggleBaseStyle

### Description
The name of the CSS class to apply to this ToggleSwitch - the actual styleName applied will be suffixed "On" or "Off", depending on the widget's current value.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.toggleOnThumbClick

### Description
When set to true, causes the ToggleSwitch to change value when the [thumb](#attr-toggleswitchthumb) is clicked, as well as when clicking in the widget body.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.thumb

### Description
A canvas used as the thumb of this ToggleSwitch, which can be styled using [ToggleSwitch.thumbBaseStyle](#attr-toggleswitchthumbbasestyle) and otherwise modified according to the AutoChild pattern - `thumbConstructor`, `thumbDefaults` and `thumbProperties` are valid.

**Flags**: IRW

---
## Attr: ToggleSwitch.toggleOnKeypress

### Description
When set to true, the value can be toggled by pressing the _Spacebar_, or changed with the left and right arrow-keys.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.animateThumb

### Description
When set to true, animates the movement of the [thumb](#attr-toggleswitchthumb) when the value changes.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToggleSwitch.value

### Description
The current value of this ToggleSwitch.

### Groups

- appearance

**Flags**: IRW

---
## Method: ToggleSwitch.setValue

### Description
Sets the [ToggleSwitch.value](#attr-toggleswitchvalue) of this ToggleSwitch.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Boolean](#type-boolean) | false | — | new value for the ToggleSwitch |

---
## Method: ToggleSwitch.valueChanged

### Description
Notification fired when the value is toggled by the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Boolean](#type-boolean) | false | — | new value for the ToggleSwitch |
| oldValue | [Boolean](#type-boolean) | false | — | previous value for the ToggleSwitch |

**Flags**: A

---
## Method: ToggleSwitch.getValue

### Description
Returns the current [ToggleSwitch.value](#attr-toggleswitchvalue) of this ToggleSwitch.

### Returns

`[Boolean](#type-boolean)` — current value of the ToggleSwitch

---
