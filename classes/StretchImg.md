# StretchImg Documentation

[← Back to API Index](../main.md)

---

## Class: StretchImg

*Inherits from:* [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas)

### Description
The StretchImg widget class implements a widget type that displays a list of multiple images that make up a single image.

---
## Attr: StretchImg.ignoreRTL

### Description
Should the [items](#attr-stretchimgitems) for this StretchImg display left-to-right even if this page is displaying [right to left text](Page.md#classmethod-pageisrtl)?

Only has an effect if this StretchImg is horizontal ([vertical](#attr-stretchimgvertical) is set to false).

Having this property set to true is usually desirable for the common pattern of media consisting of fixed size "end caps" and a stretchable center, because it allows the same media to be used for LTR and RTL pages.

If set to false, items will be displayed in RTL order for RTL pages.

### Groups

- RTL
- appearance

**Flags**: IRW

---
## Attr: StretchImg.src

### Description
The base URL for the image.

The [State](../main.md#type-state) for the component will be combined with this URL using the same approach as described in [Img.src](Img.md#attr-imgsrc). Then the image segment [name](StretchItem.md#attr-stretchitemname) as specified by each [StretchItem](../main_2.md#object-stretchitem) is added.

For example, for a stretchImg in "Over" state with a `src` of "button.png" and a segment name of "stretch", the resulting URL would be "button\_Over\_stretch.png".

### Groups

- appearance

### See Also

- [StretchImg.hSrc](#attr-stretchimghsrc)
- [StretchImg.vSrc](#attr-stretchimgvsrc)

**Flags**: IRW

---
## Attr: StretchImg.gripImgSuffix

### Description
Suffix used the 'grip' image if [StretchImg.showGrip](#attr-stretchimgshowgrip) is true.

### Groups

- grip

**Flags**: IRA

---
## Attr: StretchImg.capSize

### Description
If the default items are used, capSize is the size in pixels of the first and last images in this stretchImg.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImg.showRollOverGrip

### Description
If [StretchImg.showGrip](#attr-stretchimgshowgrip) is true, this property determines whether to show the 'Over' state on the grip image when the user rolls over on this widget. Has no effect if [StatefulCanvas.showRollOver](StatefulCanvas.md#attr-statefulcanvasshowrollover) is false.

### Groups

- grip

**Flags**: IRA

---
## Attr: StretchImg.showGrip

### Description
Should we show a "grip" image floating above the center of this widget?

### Groups

- grip

**Flags**: IRA

---
## Attr: StretchImg.items

### Description
The list of images to display as an array of objects specifying the image names and sizes.

The [name](StretchItem.md#attr-stretchitemname) is appended as a suffix to the [StretchImg.src](#attr-stretchimgsrc) URL in order to fetch separate media files for each image. Alternatively a StretchItem may specify its own [src](StretchItem.md#attr-stretchitemsrc).

The [height](StretchItem.md#attr-stretchitemheight) and [width](StretchItem.md#attr-stretchitemwidth) can be set to a number, "\*" (remaining space, divided amongst all images that specify "\*") or to the name of a property on this StretchImg component, such as "capSize" for the [StretchImg.capSize](#attr-stretchimgcapsize).

Height or width is only used for the axis along which images are stacked. For example, if [StretchImg.vertical](#attr-stretchimgvertical) is true, images stack vertically and heights are used to size images on the vertical axis, but all images will have width matching the overall component size.

For example, the default setting for `items`, which is used to produce stretchable buttons and headers with fixed-size endcaps, is as follows:

```
   items:[
        {height:"capSize", name:"start", width:"capSize"},
        {height:"*", name:"stretch", width:"*"},
        {height:"capSize", name:"end", width:"capSize"}
   ]
 
```
Note that by default horizontal StretchImg instances will always render their items in left-to-right order, even if the page is localized for right-to-left display (see [Page.isRTL](Page.md#classmethod-pageisrtl)). This default behavior may be overridden by setting the [StretchImg.ignoreRTL](#attr-stretchimgignorertl) flag to false.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImg.itemBaseStyle

### Description
If specified this css class will be applied to the individual item images within this StretchImg. May be overridden by specifying item-specific base styles to each object in the [items array](#attr-stretchimgitems). This base style will have standard stateful suffixes appended to indicate the state of this component (as described in [StatefulCanvas.baseStyle](StatefulCanvas.md#attr-statefulcanvasbasestyle)).

**Flags**: IRW

---
## Attr: StretchImg.showDownGrip

### Description
If [StretchImg.showGrip](#attr-stretchimgshowgrip) is true, this property determines whether to show the 'Down' state on the grip image when the user mousedown's on this widget. Has no effect if [StatefulCanvas.showDown](StatefulCanvas.md#attr-statefulcanvasshowdown) is false.

### Groups

- grip

**Flags**: IRA

---
## Attr: StretchImg.vSrc

### Description
Base URL for the image if [StretchImg.vertical](#attr-stretchimgvertical) is true and [StretchImg.src](#attr-stretchimgsrc) is unset.

### Groups

- appearance

### See Also

- [StretchImg.src](#attr-stretchimgsrc)
- [StretchImg.vSrc](#attr-stretchimgvsrc)

**Flags**: IRW

---
## Attr: StretchImg.showTitle

### Description
Determines whether any specified [title](StatefulCanvas.md#method-statefulcanvasgettitle) will be displayed for this component.  
Applies to Image-based components only, where the title will be rendered out in a label floating over the component

**Flags**: IRWA

---
## Attr: StretchImg.imageType

### Description
Indicates whether the image should be tiled/cropped, stretched, or centered when the size of this widget does not match the size of the image. See ImageStyle for details.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImg.hSrc

### Description
Base URL for the image if [StretchImg.vertical](#attr-stretchimgvertical) is false and [StretchImg.src](#attr-stretchimgsrc) is unset.

### Groups

- appearance

### See Also

- [StretchImg.src](#attr-stretchimgsrc)
- [StretchImg.vSrc](#attr-stretchimgvsrc)

**Flags**: IRW

---
## Attr: StretchImg.vertical

### Description
Indicates whether the list of images is drawn vertically from top to bottom (true), or horizontally from left to right (false).

### Groups

- appearance

**Flags**: IRW

---
## Method: StretchImg.setIgnoreRTL

### Description
Setter for [StretchImg.ignoreRTL](#attr-stretchimgignorertl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ignoreRTL | [boolean](../main.md#type-boolean) | false | — | new value for ignoreRTL. |

**Flags**: A

---
## Method: StretchImg.setItems

### Description
Setter for [StretchImg.items](#attr-stretchimgitems).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| items | [Array of StretchItem](#type-array-of-stretchitem) | false | — | the new array of items. |

**Flags**: A

---
## Method: StretchImg.setState

### Description
Set the specified image's state to newState and update the displayed image given by whichPart, or set the state for all images to newState and update the displayed images if whichPart is not provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newState | [String](#type-string) | false | — | name for the new state ("off", "down", etc) |
| whichPart | [String](#type-string) | true | — | name of the piece to set ("start", "stretch" or "end") if not specified, sets them all |

### Groups

- appearance

---
## Method: StretchImg.setSrc

### Description
Changes the base [StretchImg.src](#attr-stretchimgsrc) for this stretchImg, redrawing if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [SCImgURL](../main.md#type-scimgurl) | false | — | new URL for the image |

### Groups

- appearance

---
