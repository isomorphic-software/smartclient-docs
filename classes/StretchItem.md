# StretchItem Documentation

[← Back to API Index](../reference.md)

---

## Attr: StretchItem.vSrc

### Description
The URL of the media file for this StretchItem if the parent [StretchImg](StretchImg.md#class-stretchimg) is [vertical](StretchImg.md#attr-stretchimgvertical) and [StretchItem.src](#attr-stretchitemsrc) is unset.

**Flags**: IR

---
## Attr: StretchItem.src

### Description
The URL of the media file for this StretchItem.

**Flags**: IR

---
## Attr: StretchItem.width

### Description
The width of the image. This can either be a number (for the number of pixels wide), the string "\*" (remaining space, divided amongst all items that specify width:"\*"), or the name of a property on the StretchImg component, such as "capSize" for the StretchImg's [capSize](StretchImg.md#attr-stretchimgcapsize).

**NOTE:** The width is only used if the StretchImg stacks its images horizontally ([StretchImg.vertical](StretchImg.md#attr-stretchimgvertical) is false).

**Flags**: IR

---
## Attr: StretchItem.height

### Description
The height of the image. This can either be a number (for the number of pixels tall), the string "\*" (remaining space, divided amongst all items that specify height:"\*"), or the name of a property on the StretchImg component, such as "capSize" for the StretchImg's [capSize](StretchImg.md#attr-stretchimgcapsize).

**NOTE:** The height is only used if the StretchImg stacks its images vertically ([StretchImg.vertical](StretchImg.md#attr-stretchimgvertical) is true).

**Flags**: IR

---
## Attr: StretchItem.name

### Description
A string that is appended as a suffix to the StretchImg's [src](StretchImg.md#attr-stretchimgsrc) URL in order to fetch the media file for this StretchItem, if a separate [StretchItem.src](#attr-stretchitemsrc) is not provided. Note that the special name "blank", possibly suffixed by one or more digits which are used to differentiate blank items, means no image will be shown for this StretchItem.

For example, for a StretchImg in "Over" state with a [StretchImg.src](StretchImg.md#attr-stretchimgsrc) of "button.png" and a name of "stretch", the resulting URL would be "button\_Over\_stretch.png".

**Flags**: IR

---
## Attr: StretchItem.hSrc

### Description
The URL of the media file for this StretchItem if the parent [StretchImg](StretchImg.md#class-stretchimg) is [not vertical](StretchImg.md#attr-stretchimgvertical) and [StretchItem.src](#attr-stretchitemsrc) is unset.

**Flags**: IR

---
