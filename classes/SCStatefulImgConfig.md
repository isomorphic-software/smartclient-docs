# SCStatefulImgConfig Documentation

[← Back to API Index](../main.md)

---

## Attr: SCStatefulImgConfig.Selected

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig._base

### Description
The base filename for the image. This will be used if no state is applied to the stateful component displaying this image, or if no explicit entry exists for a state that is applied.  
It will also be used as a base file name for entries specified using the `"#modifier:_some_value_"` format.

In some cases, an icon may have only custom states - for example, a tree-folder icon is always either opened or closed, so a `_base` entry is not required unless entries in the object use the _#state_ or _#modifier_ components - in this case, a warning will be logged if no `_base` is set.

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.SelectedDown

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected) on [mouse down](StatefulCanvas.md#attr-statefulcanvasshowdown).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.SelectedOver

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected) on [roll over](StatefulCanvas.md#attr-statefulcanvasshowrollover).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.FocusedOver

### Description
Image to display when the component is [focused](Canvas.md#method-canvasisfocused) on [roll over](StatefulCanvas.md#attr-statefulcanvasshowrollover).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.Down

### Description
Image to display on [mouseDown](StatefulCanvas.md#attr-statefulcanvasshowdown).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.SelectedFocused

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected) and [focused](Canvas.md#method-canvasisfocused).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.Over

### Description
Image to display on [roll over](StatefulCanvas.md#attr-statefulcanvasshowrollover).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.SelectedFocusedOver

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected) and [focused](Canvas.md#method-canvasisfocused) on [roll over](StatefulCanvas.md#attr-statefulcanvasshowrollover).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.SelectedFocusedDown

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected) and [focused](Canvas.md#method-canvasisfocused) on [mouse down](StatefulCanvas.md#attr-statefulcanvasshowdown).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.Focused

### Description
Image to display when the component is [focused](Canvas.md#method-canvasisfocused).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.FocusedDown

### Description
Image to display when the component is [focused](Canvas.md#method-canvasisfocused) on [mouse down](StatefulCanvas.md#attr-statefulcanvasshowdown).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.Disabled

### Description
Image to display when the component is [disabled](Canvas.md#attr-canvasdisabled).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
## Attr: SCStatefulImgConfig.SelectedDisabled

### Description
Image to display when the component is [selected](StatefulCanvas.md#attr-statefulcanvasselected) and [disabled](Canvas.md#attr-canvasdisabled).

May be specified as

*   A [SCImgURL](../main.md#type-scimgurl) indicating the media to load
*   A reference to another entry in this SCStatefulImgConfig via the format `"#state:_otherStateName_"`
*   A modifier to apply to the [SCStatefulImgConfig._base](#attr-scstatefulimgconfig_base) media via the format `"#modifier:_modifierString_"`

See [SCStatefulImgConfig overview](../main.md#object-scstatefulimgconfig) for further information.

**Flags**: IRW

---
