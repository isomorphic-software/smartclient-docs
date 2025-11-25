# DrawKnob Documentation

[← Back to API Index](../main.md)

---

## Class: DrawKnob

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Canvas that renders a [DrawItem](DrawItem.md#class-drawitem) into a [DrawPane](DrawPane.md#class-drawpane) and provides interactivity for that drawItem, including drag and drop.

A DrawKnob can either be initialized with a [DrawItem knobShape](#attr-drawknobknobshape) or created via the [AutoChild](../main.md#type-autochild) pattern.

DrawKnobs are used by the [drawItem control knobs](DrawItem.md#attr-drawitemknobs) subsystem.

---
## Attr: DrawKnob.knobShape

### Description
The [DrawItem](DrawItem.md#class-drawitem) instance rendered into this DrawKnob's drawPane

**Flags**: R

---
## Attr: DrawKnob.y

### Description
Y-Coordinate for this DrawKnob. DrawKnob will initially be drawn centered over this coordinate

**Flags**: IR

---
## Attr: DrawKnob.knobShapeDefaults

### Description
Default properties for this component's [DrawKnob.knobShape](#attr-drawknobknobshape). Has the following properties by default:
```
  radius : 5,
  lineWidth:2,
  fillColor:"#FF0000",
  fillOpacity:0.5,
 
```
As with any auto-child defaults block, use [Class.changeDefaults](Class.md#classmethod-classchangedefaults) to modify this object.

**Flags**: IRA

---
## Attr: DrawKnob.drawPane

### Description
[DrawPane](DrawPane.md#class-drawpane) into which this DrawKnob's [DrawKnob.knobShape](#attr-drawknobknobshape) will be rendered.

**Flags**: IR

---
## Attr: DrawKnob.x

### Description
X-Coordinate for this DrawKnob. DrawKnob will initially be drawn centered over this coordinate

**Flags**: IR

---
## Method: DrawKnob.updatePoints

### Description
Method called in response to the user dragging this DrawKnob. May be observed or overridden to allow drawItems to react to user drag interactions on this knob.

Note that the default implementation does nothing. When working with draw knobs directly this is typically where you would both update the shape being controlled by the draw knob, and ensure the drawKnob gets repositioned. You may also need to update the drawKnob position in response to the drawItem being repositioned, resized, etc.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | false | — | new x-coordinate of the drawKnob |
| y | [Integer](../main_2.md#type-integer) | false | — | new y-coordinate of the drawKnob |
| dX | [Integer](../main_2.md#type-integer) | false | — | horizontal distance moved |
| dY | [Integer](../main_2.md#type-integer) | false | — | vertical distance moved |
| state | [String](#type-string) | false | — | either "start", "move", or "stop", to indicate the current phase of dragging of the DrawKnob for which the points need to be updated |

---
## Method: DrawKnob.setCenterPoint

### Description
Sets the center point of the drawKnob. If the optional `viewboxCoords` argument is passed, coordinates are expected to be adjusted for drawPane pan and zoom. Otherwise coordinates are expected to be absolute pixel coordinates within the drawPane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | false | — | new x coordinate for this drawKnob |
| y | [Integer](../main_2.md#type-integer) | false | — | new y coordinate for this drawKnob |
| viewboxCoords | [boolean](../main.md#type-boolean) | true | — | If `true`, the `x` and `y` values are expected to be in the viewbox coordinate system (described [here](DrawPane.md#class-drawpane)) - already adjusted for any zoom or pan applied to the drawPane. |

---
