# DrawGroup Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawGroup

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to manage a group of other DrawItem instances.

A DrawGroup has no local visual representation other than that of its drawItems. Adding items to a drawGroup allows for central event handling, and allows them to be manipulated (drawn, scaled, etc) together.

DrawItems are added to a DrawGroup by creating the DrawItems with [DrawItem.drawGroup](DrawItem.md#attr-drawitemdrawgroup) set to the DrawGroup, or by creating a DrawGroup with [DrawGroup.drawItems](#attr-drawgroupdrawitems).

DrawGroups handle events by having an explicitly specified group rectangle (see [DrawGroup.getGroupRect](#method-drawgroupgetgrouprect)). This rectangle has no visual representation within the draw pane (is not visible) but any user-interactions within the specified coordinates will trigger group level events.

DrawGroups may contain other DrawGroups.

---
## Attr: DrawGroup.width

### Description
Width of the [group rectangle](#method-drawgroupgetgrouprect) in pixels relative to the [DrawPane](DrawPane.md#class-drawpane) (the "drawing coordinate system").

**Flags**: IRW

---
## Attr: DrawGroup.drawItems

### Description
Initial list of DrawItems for this DrawGroup.

DrawItems can be added to a DrawGroup after initialization by setting [DrawItem.drawGroup](DrawItem.md#attr-drawitemdrawgroup).

**Flags**: IR

---
## Attr: DrawGroup.knobs

### Description
DrawGroup only supports the "move" knob type.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)
- [DrawGroup.moveItemsWithGroup](#attr-drawgroupmoveitemswithgroup)

**Flags**: IR

---
## Attr: DrawGroup.showGroupRectOutline

### Description
If the "move" [control knob](DrawItem.md#attr-drawitemknobs) is shown for this group and [useGroupRect](#attr-drawgroupusegrouprect) is true, should the [DrawGroup.groupRectOutline](#attr-drawgroupgrouprectoutline) be shown?

Set to false to disable showing the `groupRectOutline`.

**Flags**: IRW

---
## Attr: DrawGroup.moveItemsWithGroup

### Description
Should dragging the group (when [canDrag](DrawItem.md#attr-drawitemcandrag) is true) or dragging the move knob also move the items within this `DrawGroup`?

**Flags**: IRWA

---
## Attr: DrawGroup.groupRectOutline

### Description
If this group is showing a "move" [control knob](DrawItem.md#attr-drawitemknobs), the `groupRectOutline` is a [DrawRect](DrawRect.md#class-drawrect) AutoChild that identifies the group's group rect (see [DrawGroup.useGroupRect](#attr-drawgroupusegrouprect)).

`useGroupRect` must be true and the "move" control knob must be showing for the `groupRectOutline` AutoChild to be created and shown.

**Flags**: IR

---
## Attr: DrawGroup.useGroupRect

### Description
When should this drawGroup receive event notifications? If set to `true`, the developer can specify an explicit [set of coordinates](#method-drawgroupgetgrouprect). Whenever the user interacts with this rectangle, the drawGroup will be notified and the appropriate event handlers will be fired. Note that rectangle need not contain all DrawItems within the group, and is manually managed by the developer.  
If set to `false`, the [event rectangle](#method-drawgroupgetgrouprect) coordinates are unused - instead as a user interacts with specific drawItems within this group, the appropriate event handler would be fired on the item, then the event would "bubble" to the drawGroup, firing the appropriate event handler at the group level as well.

**Flags**: IR

---
## Attr: DrawGroup.left

### Description
Left coordinate of the [group rectangle](#method-drawgroupgetgrouprect) in pixels relative to the [DrawPane](DrawPane.md#class-drawpane) (the "drawing coordinate system").

**Flags**: IRW

---
## Attr: DrawGroup.height

### Description
Height of the [group rectangle](#method-drawgroupgetgrouprect) in pixels relative to the [DrawPane](DrawPane.md#class-drawpane) (the "drawing coordinate system").

**Flags**: IRW

---
## Attr: DrawGroup.top

### Description
Top coordinate of the [group rectangle](#method-drawgroupgetgrouprect) in pixels relative to the [DrawPane](DrawPane.md#class-drawpane) (the "drawing coordinate system").

**Flags**: IRW

---
## Method: DrawGroup.scaleBy

### Description
Scale all drawItem\[\] shapes by the x, y multipliers

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [float](../reference.md#type-float) | false | — | scale in the x direction |
| y | [float](../reference.md#type-float) | false | — | scale in the y direction |

---
## Method: DrawGroup.scaleTo

### Description
Scale the each item in the drawGroup by the x, y multipliers

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [float](../reference.md#type-float) | false | — | scale in the x direction |
| y | [float](../reference.md#type-float) | false | — | scale in the y direction |

---
## Method: DrawGroup.moveBy

### Description
Updates the `DrawGroup`'s left coordinate by `dX` and the top coordinate by `dY`. Note that this does not move or resize the items in this `DrawGroup`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | change to left coordinate in pixels |
| dY | [Distance](../reference.md#type-distance) | false | — | change to top coordinate in pixels |

---
## Method: DrawGroup.erase

### Description
Erases all DrawItems in the DrawGroup.

---
## Method: DrawGroup.dragMove

### Description
Notification fired for every mouseMove event triggered while the user is dragging this DrawGroup. Will only fire if [canDrag](DrawItem.md#attr-drawitemcandrag) is true for this group.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

Default drag behavior will be to reposition all items in the group (and update the group rectangle).

### Returns

`[Boolean](#type-boolean)` — false to cancel drag interaction.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.getBoundingBox

### Description
Returns the left, top, (left + width), and (top + height) values

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawGroup.mouseMove

### Description
Notification fired when the user moves the mouse over this DrawGroup.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.click

### Description
Notification fired when the user clicks on this DrawGroup.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.setHeight

### Description
Sets the height of this `DrawGroup`'s [group rectangle](#method-drawgroupgetgrouprect). Note that setting the height will not move or resize the items in this `DrawGroup`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Distance](../reference.md#type-distance) | false | — | new height for the group rectangle |

---
## Method: DrawGroup.mouseUp

### Description
Notification fired when the user releases the left mouse button on this DrawGroup.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.setTop

### Description
Sets the top coordinate of this `DrawGroup`'s [group rectangle](#method-drawgroupgetgrouprect). Note that setting the top coordinate will not move the items in this `DrawGroup`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| top | [Coordinate](../reference.md#type-coordinate) | false | — | new top coordinate in pixels |

---
## Method: DrawGroup.setWidth

### Description
Sets the width of this `DrawGroup`'s [group rectangle](#method-drawgroupgetgrouprect). Note that setting the width will not move or resize the items in this `DrawGroup`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Distance](../reference.md#type-distance) | false | — | new width for the group rectangle |

---
## Method: DrawGroup.getCenter

### Description
Get the center point of the [group rectangle](#method-drawgroupgetgrouprect).

### Returns

`[Point](#type-point)` — the center point

---
## Method: DrawGroup.rotateBy

### Description
Rotate each item in the group by the specified number of degrees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degrees | [float](../reference.md#type-float) | false | — | — |

---
## Method: DrawGroup.mouseOver

### Description
Notification fired when the mouse enters this DrawGroup.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.getGroupRect

### Description
This method will return an array of integers (left, top, width, height) defining the area of the "group rectangle" for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is true, this is the area of the DrawPane where user interactions will fire event notifications on this DrawGroup.

This is a convienence method to get the current coordinates of the [group rectangle](#attr-drawgroupusegrouprect). Developers must use [DrawGroup.setLeft](#method-drawgroupsetleft), [DrawGroup.setTop](#method-drawgroupsettop), [DrawGroup.setWidth](#method-drawgroupsetwidth) or [DrawGroup.setHeight](#method-drawgroupsetheight) to set each coordinate directly.

### Returns

`[Array of int](#type-array-of-int)` — 4 element array containing left, top, width, height of the group rectangle.

---
## Method: DrawGroup.moveTo

### Description
Sets both the left and top coordinates of this `DrawGroup`'s [group rectangle](#method-drawgroupgetgrouprect). Note that this does not move or resize the items in this `DrawGroup`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate in pixels |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate in pixels |

---
## Method: DrawGroup.dragStart

### Description
Notification fired when the user starts to drag this DrawGroup. Will only fire if [canDrag](DrawItem.md#attr-drawitemcandrag) is true for this group.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

Default drag behavior will be to reposition all items in the group (and update the group rectangle).

### Returns

`[Boolean](#type-boolean)` — false to cancel drag action.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.mouseDown

### Description
Notification fired when the user presses the left mouse button on this DrawGroup.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawGroup.setLeft

### Description
Sets the left coordinate of this `DrawGroup`'s [group rectangle](#method-drawgroupgetgrouprect). Note that setting the left coordinate will not move the items in this `DrawGroup`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../reference.md#type-coordinate) | false | — | new left coordinate |

---
## Method: DrawGroup.rotateTo

### Description
Rotate each item in the group to the specified number of degrees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degrees | [float](../reference.md#type-float) | false | — | — |

---
## Method: DrawGroup.mouseOut

### Description
Notification fired when the mouse leaves this DrawGroup.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

---
## Method: DrawGroup.dragStop

### Description
Notification fired when the user stops dragging this DrawGroup. Will only fire if [canDrag](DrawItem.md#attr-drawitemcandrag) is true for this group.

Note that if [useGroupRect](#attr-drawgroupusegrouprect) is true, this notification will be triggered by the user interacting with the specified [group rectangle](#method-drawgroupgetgrouprect) for the group. If [useGroupRect](#attr-drawgroupusegrouprect) is false, the notification will bubble up from interactions with individual items within the group.

### Returns

`[Boolean](#type-boolean)` — false to cancel drag interaction.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
