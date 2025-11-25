# Stateful Images

[← Back to API Index](../main.md)

---

## KB Topic: Stateful Images

### Description
Images displayed in [stateful components](../classes/StatefulCanvas.md#class-statefulcanvas) may display different media depending on the current state of the component. See the [Img.src](../classes/Img.md#attr-imgsrc) attribute or [Button.icon](../classes/Button.md#attr-buttonicon) attribute for examples of such "stateful images".

In general the media to load for each state may be specified in two ways:

#### Base URL combined with state suffixes
If the property in question is set to a standard [image URL](../main.md#type-scimgurl), this value will be treated as a default, or base URL. When a new [state](../classes/StatefulCanvas.md#attr-statefulcanvasstate) is applied, this filename will be combined with the state name to form a combined URL. This in turn changes the media that gets loaded and updates the image to reflect the new state.  
Note that if the property was defined as a sprite configuration string a css style may be defined instead of, or in addition to a src URL. See the [sprite configuration documentation](../main.md#type-scspriteconfig) for a discussion of how sprites can be used for stateful images.

The following table lists out the standard set of combined URLs that may be generated. Subclasses may support additional state-derived media of course. Note that the src URL will be split such that the extension is always applied to the end of the combined string. For example in the following table, if `src` was set to `"blank.gif"`, the Selected+Focused URL would be `"blank_Selected_Focused.gif"`.

| URL for Img source | Description |
|---|---|
| src+extension | Default URL |
| src+"_Selected"+extension | Applied when [StatefulCanvas.selected](../classes/StatefulCanvas.md#attr-statefulcanvasselected) is set to true |
| src+"_Focused"+extension | Applied when the component has keyboard focus, if [StatefulCanvas.showFocused](../classes/StatefulCanvas.md#attr-statefulcanvasshowfocused) is true, and [StatefulCanvas.showFocusedAsOver](../classes/StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is not true. |
| src+"_Over"+extension | Applied when the user rolls over the component if [StatefulCanvas.showRollOver](../classes/StatefulCanvas.md#attr-statefulcanvasshowrollover) is set to true |
| src+"_Down"+extension | Applied when the user presses the mouse button over over the component if [StatefulCanvas.showDown](../classes/StatefulCanvas.md#attr-statefulcanvasshowdown) is set to true |
| src+"_Disabled"+extension | Applied to [Canvas.disabled](../classes/Canvas.md#attr-canvasdisabled) component if [StatefulCanvas.showDisabled](../classes/StatefulCanvas.md#attr-statefulcanvasshowdisabled) is true. |
| Combined states |
| src+"_Selected_Focused"+extension | Combined Selected and focused state |
| src+"_Selected_Over"+extension | Combined Selected and rollOver state |
| src+"_Focused_Over"+extension | Combined Focused and rollOver state |
| src+"_Selected_Focused_Over"+extension | Combined Selected, Focused and rollOver state |
| src+"_Selected_Down"+extension | Combined Selected and mouse-down state |
| src+"_Focused_Down"+extension | Combined Focused and mouse-down state |
| src+"_Selected_Focused_Down"+extension | Combined Selected, Focused and mouse-down state |
| src+"_Selected_Disabled"+extension | Combined Selected and Disabled state |

#### Explicit stateful image configuration
The [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig) object allows developers to specify a set of explicit image URLs, one for each state to be displayed, rather than relying on an automatically generated combined URL. This pattern is useful for cases where the filename of the stateful versions of the image doesn't match up with the auto-generated format.

---
