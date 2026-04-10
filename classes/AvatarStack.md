# AvatarStack Documentation

[← Back to API Index](../reference.md)

---

## Class: AvatarStack

*Inherits from:* [HLayout](../reference.md#class-hlayout)

### Description
A layout that displays a row of overlapping circular avatar images, commonly used for showing team members or assignees. This is not achievable via CSS alone because it must manage overlapping z-index ordering, handle click on individual avatars, and show a "+N more" overflow indicator.

---
## Attr: AvatarStack.avatars

### Description
Array of image URLs for the avatars to display.

**Flags**: IRW

---
## Attr: AvatarStack.avatarSize

### Description
Diameter of each avatar circle in pixels.

**Flags**: IR

---
## Attr: AvatarStack.maxVisible

### Description
Maximum avatars before the "+N" overflow indicator.

**Flags**: IR

---
## Attr: AvatarStack.overlap

### Description
Pixels each avatar overlaps its predecessor.

**Flags**: IR

---
## Method: AvatarStack.setAvatars

### Description
Set the array of avatar image URLs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| urls | [Array of String](#type-array-of-string) | false | — | image URLs |

---
