# NavigationBar Documentation

[← Back to API Index](../reference.md)

---

## Class: NavigationBar

*Inherits from:* [HLayout](../reference.md#class-hlayout)

### Description
Navigation control implemented as a horizontal layout showing back and forward controls and a title.

---
## Attr: NavigationBar.rightButton

### Description
The button displayed to the right of the title in this NavigationBar. By default this will be a [NavigationButton](NavigationButton.md#class-navigationbutton) with [direction](NavigationButton.md#attr-navigationbuttondirection) set to `"forward"`.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [rightButtonTitle](#attr-navigationbarrightbuttontitle) for [Button.title](Button.md#attr-buttontitle)
*   [rightButtonIcon](#attr-navigationbarrightbuttonicon) for [Button.icon](Button.md#attr-buttonicon)

### See Also

- [NavigationBar.showRightButton](#attr-navigationbarshowrightbutton)

**Flags**: IR

---
## Attr: NavigationBar.shortLeftButtonTitle

### Description
Short title to display for the left button title if there is not enough room to show the title for the navigation bar. Setting to null or an empty string ("") will avoid a shortened title ever being used. See [NavigationBar.title](#attr-navigationbartitle) for a full description.

**Flags**: IRW

---
## Attr: NavigationBar.rightButtonTitle

### Description
[Title](Button.md#attr-buttontitle) for the [rightButton](#attr-navigationbarrightbutton).

**Flags**: IRW

---
## Attr: NavigationBar.animateStateChanges

### Description
Whether to animate a change of the view state via [NavigationBar.setViewState](#method-navigationbarsetviewstate).

Enabling animation of state changes does have a performance impact because more components need to be created by the `NavigationBar` to implement the animated transitions. It is therefore recommended to leave `animateStateChanges` at its default value of `false` unless [NavigationBar.setViewState](#method-navigationbarsetviewstate) might be called on this `NavigationBar` instance and animation is desired.

Note also that when animation is enabled, certain AutoChild defaults and properties may be used to create other AutoChildren that are internal to the animation implementation. This generally does not cause an issue unless certain non-UI event handlers are added to the defaults and/or properties (e.g. [Canvas.visibilityChanged](Canvas.md#method-canvasvisibilitychanged), [Canvas.resized](Canvas.md#method-canvasresized)). For those types of handlers, a check should be added to make sure that the handler is running for the expected component.

**Flags**: IRA

---
## Attr: NavigationBar.leftButtonTitle

### Description
[Title](Button.md#attr-buttontitle) for the [leftButton](#attr-navigationbarleftbutton).

**Flags**: IRW

---
## Attr: NavigationBar.alwaysShowLeftButtonTitle

### Description
If set, the left button title will never be omitted in an attempt to fit the full title. See the documentation of [NavigationBar.title](#attr-navigationbartitle) for details.

**Flags**: IRW

---
## Attr: NavigationBar.showLeftButton

### Description
If set to `false`, then the [leftButton](#attr-navigationbarleftbutton) is not shown.

**Flags**: IRW

---
## Attr: NavigationBar.leftButtonIcon

### Description
[Icon](Button.md#attr-buttonicon) for the [leftButton](#attr-navigationbarleftbutton).

**Flags**: IRW

---
## Attr: NavigationBar.leftButton

### Description
The button displayed to the left of the title in this NavigationBar. By default this will be a [NavigationButton](NavigationButton.md#class-navigationbutton) with [direction](NavigationButton.md#attr-navigationbuttondirection) set to "back".

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [leftButtonTitle](#attr-navigationbarleftbuttontitle) for [Button.title](Button.md#attr-buttontitle)
*   [leftButtonIcon](#attr-navigationbarleftbuttonicon) for [Button.icon](Button.md#attr-buttonicon)

### See Also

- [NavigationBar.showLeftButton](#attr-navigationbarshowleftbutton)

**Flags**: IR

---
## Attr: NavigationBar.showRightButton

### Description
If set to `false`, then the [rightButton](#attr-navigationbarrightbutton) is not shown.

**Flags**: IRW

---
## Attr: NavigationBar.miniNavControl

### Description
AutoChild of type [MiniNavControl](../reference.md#class-mininavcontrol). Not shown by default (see [showMiniNavControl](#attr-navigationbarshowmininavcontrol)). Also, if a [customNavControl](#attr-navigationbarcustomnavcontrol) is provided, then the `customNavControl` is used instead of an automatically created `miniNavControl`.

**Flags**: IR

---
## Attr: NavigationBar.customNavControl

### Description
An arbitrary component that will be placed where the [miniNavControl](#attr-navigationbarmininavcontrol) AutoChild would normally be placed (see [miniNavAlign](#attr-navigationbarmininavalign)).

**Flags**: IRW

---
## Attr: NavigationBar.titleLabel

### Description
The AutoChild label used to display the [title](#attr-navigationbartitle) in this NavigationBar.

**Flags**: IR

---
## Attr: NavigationBar.rightButtonIcon

### Description
[Icon](Button.md#attr-buttonicon) for the [rightButton](#attr-navigationbarrightbutton).

**Flags**: IRW

---
## Attr: NavigationBar.title

### Description
The title to display in the center of this navigation bar.

If there is not enough room for the title with the current titles of the [left](#attr-navigationbarleftbutton) and [right](#attr-navigationbarrightbutton) buttons, space will be used as follows:

*   if the title can be fully visible without clipping if it is placed slightly off-center, it will be placed off-center, up to a maximum of [maxCenterOffset](#attr-navigationbarmaxcenteroffset) pixels
*   if that's not enough space, if a [shortLeftButtonTitle](#attr-navigationbarshortleftbuttontitle) is provided, it will be used in lieu of the normal left button title
*   if that's still not enough space, the title of the left button will be hidden, leaving only the icon. This will be skipped if either [alwaysShowLeftButtonTitle](#attr-navigationbaralwaysshowleftbuttontitle) has been set or the button has no icon, which would leave the space blank.
*   if that's still not enough space, the title text will be clipped, showing an ellipsis (where browser support allows this)

**Flags**: IRW

---
## Attr: NavigationBar.miniNavAlign

### Description
Placement of [MiniNavControl](../reference.md#class-mininavcontrol), if present:

*   "right" alignment places the miniNav on the far right
*   "center" alignment places the miniNav in the center, or to the right of the title if the title is present
*   "left" alignment will place the miniNav on the left, or to the right of the [NavigationBar.leftButton](#attr-navigationbarleftbutton) if its present.

**Flags**: IR

---
## Attr: NavigationBar.showMiniNavControl

### Description
If set to `false`, then the [miniNavControl](#attr-navigationbarmininavcontrol) is not shown.

**Flags**: IR

---
## Attr: NavigationBar.controls

### Description
Controls to show in the navigation bar. The auto children names "leftButton", "titleLabel", "rightButton" may be used to show the standard navigation bar controls, as well as any Canvases (which will be embedded directly in the navigation bar).

**Flags**: IRW

---
## Attr: NavigationBar.maxCenterOffset

### Description
Maximum amount in pixels that the title will be placed off center in an effort to avoid clipping it - see [title](#attr-navigationbartitle).

**Flags**: IR

---
## Method: NavigationBar.setLeftButtonTitle

### Description
Setter for [leftButtonTitle](#attr-navigationbarleftbuttontitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title HTML for the left button. |

---
## Method: NavigationBar.setShowRightButton

### Description
Show or hide the [rightButton](#attr-navigationbarrightbutton). The `rightButton` must be a [control](#attr-navigationbarcontrols) of this `NavigationBar` or else it will still be hidden.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [Boolean](#type-boolean) | false | — | if `false`, then the `rightButton` will be hidden. If unset or `true` then the `rightButton` will be shown as long as it is a member of the `controls` array. |

---
## Method: NavigationBar.setTitle

### Description
Updates the [title](#attr-navigationbartitle) for this `NavigationBar`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title HTML. |

---
## Method: NavigationBar.navigationClick

### Description
Notification method fired when the user clicks the [NavigationBar.leftButton](#attr-navigationbarleftbutton) or [NavigationBar.rightButton](#attr-navigationbarrightbutton)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| direction | [NavigationDirection](../reference.md#type-navigationdirection) | false | — | direction in which the user is attempting to navigate |

---
## Method: NavigationBar.setRightButtonIcon

### Description
Setter for [rightButtonIcon](#attr-navigationbarrightbuttonicon).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newIcon | [SCImgURL](../reference_2.md#type-scimgurl) | false | — | new icon for the right button. |

---
## Method: NavigationBar.setAlwaysShowLeftButtonTitle

### Description
Setter for [alwaysShowLeftButtonTitle](#attr-navigationbaralwaysshowleftbuttontitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newAlwaysShowLeftButtonTitle | [boolean](../reference.md#type-boolean) | false | — | new value for `alwaysShowLeftButtonTitle`. |

---
## Method: NavigationBar.upClick

### Description
Notification method fired when the up button on the [miniNavControl](#attr-navigationbarmininavcontrol) is clicked.

---
## Method: NavigationBar.setRightButtonTitle

### Description
Setter for [rightButtonTitle](#attr-navigationbarrightbuttontitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title HTML for the right button. |

---
## Method: NavigationBar.setCustomNavControl

### Description
Setter to update the [NavigationBar.customNavControl](#attr-navigationbarcustomnavcontrol) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| controls | [Array of String](#type-array-of-string)|[Array of Canvas](#type-array-of-canvas) | false | — | — |

---
## Method: NavigationBar.downClick

### Description
Notification method fired when the down button on the [miniNavControl](#attr-navigationbarmininavcontrol) is clicked.

---
## Method: NavigationBar.setLeftButtonIcon

### Description
Setter for [leftButtonIcon](#attr-navigationbarleftbuttonicon).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newIcon | [SCImgURL](../reference_2.md#type-scimgurl) | false | — | new icon for left button. |

---
## Method: NavigationBar.setShortLeftButtonTitle

### Description
Setter for [shortLeftButtonTitle](#attr-navigationbarshortleftbuttontitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newShortLeftButtonTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new short title HTML. |

---
## Method: NavigationBar.setViewState

### Description
Sets multiple state attributes of this `NavigationBar` at once. If this `NavigationBar` was created with [animateStateChanges](#attr-navigationbaranimatestatechanges) set to `true`, then the change-over to the new state attributes will be animated if the direction is either "forward" or "back".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewState | [NavigationBarViewState](#type-navigationbarviewstate) | false | — | the new view state. |
| direction | [NavigationDirection](../reference.md#type-navigationdirection) | true | — | an optional direction for animation. If not specified or set to "none" then the state change will not be animated. The direction should be "forward" for operations that reveal new content and "back" for operations that reveal previously-displayed content. |

**Flags**: A

---
## Method: NavigationBar.setShowLeftButton

### Description
Show or hide the [leftButton](#attr-navigationbarleftbutton). The `leftButton` must be a [control](#attr-navigationbarcontrols) of this `NavigationBar` or else it will still be hidden.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [Boolean](#type-boolean) | false | — | if `false`, then the `leftButton` will be hidden. If unset or `true` then the `leftButton` will be shown as long as it is a member of the `controls` array. |

---
