# Scrollbar Documentation

[← Back to API Index](../reference.md)

---

## Class: Scrollbar

*Inherits from:* [StretchImg](StretchImg.md#class-stretchimg)

### Description
The Scrollbar widget implements cross-platform, image-based scrollbars that control the scrolling of content in other widgets. Scrollbar widgets are created and displayed automatically for widgets that require them, based on settings for [Canvas.overflow](Canvas.md#attr-canvasoverflow).

The scrollbar's appearance is based on a [StretchImg](StretchImg.md#class-stretchimg) for the "track", which consists of two fixed size buttons and a stretchable center segment, and the [ScrollThumb](../reference.md#class-scrollthumb), the draggable portion of the scrollbar, also a StretchImg, with an optional [grip](StretchImg.md#attr-stretchimgshowgrip).

---
## Attr: Scrollbar.cornerSize

### Description
Allows the size of the corner segment to be set independently of the [Scrollbar.btnSize](#attr-scrollbarbtnsize).

### Groups

- corner

**Flags**: IR

---
## Attr: Scrollbar.trackEndHeight

### Description
The minimum pixel height of the track end segments (if enabled with showTrackEnds).

### Groups

- track

**Flags**: IRA

---
## Attr: Scrollbar.allowThumbDownState

### Description
If true, the thumb's appearance changes when it's clicked on.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.allowThumbOverState

### Description
If true, the thumb's appearance changes when the user rolls over it.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.trackEndImg

### Description
The StretchItem for the end of a scrollbar track. The default is: `{ name:"track_end", width:"trackEndSize", height:"trackEndSize" }`

**Flags**: IR

---
## Attr: Scrollbar.thumbInset

### Description
Inset of the thumb relative to the track. An inset of N pixels means the thumb is 2N pixels smaller in breadth than the track.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.trackStartImg

### Description
The StretchItem for the start of a scrollbar track. The default is: `{ name:"track_start", width:"trackStartSize", height:"trackStartSize" }`

**Flags**: IR

---
## Attr: Scrollbar.showTrackEnds

### Description
If true, the scrollbar uses a 5-segment rather than 3-segment image representation, where the 3 interior image segments have the same state (Down, Over, etc), independent of the two outermost image segments.

This allows certain advanced skinning designs where the track-as-such (space in which the thumb may be dragged) has curved endcaps, and is also visually stateful (that is, changes when the mouse goes down, without affecting the appearance of the outermost segments).

### Groups

- track

**Flags**: IRA

---
## Attr: Scrollbar.showTrackButtons

### Description
Should the track buttons that allow page scrolling be shown?

### Groups

- track

**Flags**: IRA

---
## Attr: Scrollbar.cornerSrc

### Description
URL for the corner image, a singular image that appears in the corner when both h and v scrollbars are showing.

### Groups

- images

**Flags**: IR

---
## Attr: Scrollbar.startThumbOverlap

### Description
Number of pixels the thumb is allowed to overlap the buttons at the start of the track. Default prevents doubling of 1px borders. Set higher to allow media that shows curved joins between the track button and ScrollThumb.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.endThumbOverlap

### Description
Number of pixels the thumb is allowed to overlap the buttons at the end of the track. Default prevents doubling of 1px borders. Set higher to allow media that shows curved joins between the track button and ScrollThumb.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.startImg

### Description
The StretchItem for the start of a scrollbar (the "scroll up" or "scroll left" button image). The default is: `{ name:"start", width:"btnSize", height:"btnSize" }`

**Flags**: IR

---
## Attr: Scrollbar.hSrc

### Description
Base URL for the images used for the horizontal scrollbar track and end buttons.

See [StretchImg.items](StretchImg.md#attr-stretchimgitems) for a general explanation of how this base URL is transformed into various pieces and states.

For a normal 3-segment track, the suffixes "\_start", "\_track" and "\_end" are added to this URL. The "start" and "end" images should appear to be buttons (the user can click on these segments to scroll slowly). The "track" segment provides a background for the space in which the thumb can be dragged, and can also be clicked on to scroll quickly.

For a 5-segment track ([Scrollbar.showTrackEnds](#attr-scrollbarshowtrackends):true), the suffixes are "\_start", "\_track\_start", "\_track", "\_track\_end" and "\_end".

### Groups

- images

**Flags**: IR

---
## Attr: Scrollbar.vSrc

### Description
Base URL for the images used for the vertical scrollbar track and end buttons. See [Scrollbar.hSrc](#attr-scrollbarhsrc) for usage.

### Groups

- images

**Flags**: IR

---
## Attr: Scrollbar.skinImgDir

### Description
Where are the skin images for the Scrollbar. This is local to the [overall skin directory](Page.md#classmethod-pagegetskindir).

### Groups

- images

**Flags**: IRA

---
## Attr: Scrollbar.endImg

### Description
The StretchItem for the end of a scrollbar (the "scroll down" or "scroll right" button image). The default is: `{ name:"end", width:"btnSize", height:"btnSize" }`

**Flags**: IR

---
## Attr: Scrollbar.scrollTarget

### Description
The widget whose contents should be scrolled by this scrollbar. The scrollbar thumb is sized according to the amount of visible vs. scrollable content in this widget.

**Flags**: IRWA

---
## Attr: Scrollbar.btnSize

### Description
The size of the square buttons (arrows) at the ends of this scrollbar. This overrides [Canvas.scrollbarSize](Canvas.md#attr-canvasscrollbarsize) to set the width of a vertical scrollbar or the height of a horizontal scrollbar. If not set it will default to [Canvas.scrollbarSize](Canvas.md#attr-canvasscrollbarsize).

### Groups

- track

**Flags**: IRW

---
## Attr: Scrollbar.trackImg

### Description
The StretchItem for the middle part of a scrollbar track, which usually takes up the majority of the width or height of the scrollbar. The default is: `{ name:"track", width:"*", height:"*" }`

**Flags**: IR

---
## Attr: Scrollbar.cornerImg

### Description
The StretchItem for the corner between vertical and horizontal scrollbars. The width and height are determined automatically, so [StretchItem.width](StretchItem.md#attr-stretchitemwidth) and [StretchItem.height](StretchItem.md#attr-stretchitemheight) set on the cornerImg StretchItem are ignored. The default is: `{ name:"corner" }`

**Flags**: IR

---
## Attr: Scrollbar.trackEndWidth

### Description
The minimum pixel width of the track end segments (if enabled with showTrackEnds).

### Groups

- track

**Flags**: IRA

---
## Attr: Scrollbar.thumbOverlap

### Description
Number of pixels the thumb is allowed to overlap the buttons at each end of the track. Default prevents doubling of 1px borders. Set higher to allow media that shows curved joins between the track button and ScrollThumb.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.thumbMinSize

### Description
The minimum pixel size of the draggable thumb regardless of how large the scrolling region becomes.

### Groups

- thumb

**Flags**: IRA

---
## Attr: Scrollbar.autoEnable

### Description
If true, this scrollbar will automatically enable when the scrollTarget is scrollable (i.e., when the contents of the scrollTarget exceed its clip size in the direction relevant to this scrollbar), and automatically disable when the scrollTarget is not scrollable. Set this property to false for full manual control over a scrollbar's enabled state.

**Flags**: IRWA

---
## Attr: Scrollbar.showCorner

### Description
If true, displays a corner piece at the bottom end of a vertical scrollbar, or the right end of a horizontal scrollbar. This is typically set only when both horizontal and vertical scrollbars are displayed and about the same corner.

### Groups

- corner

**Flags**: IRA

---
## Method: Scrollbar.setScrollTarget

### Description
Sets or clears the scrollbar's scrollTarget. If no argument is provided, then the scrollTarget will be set to the scrollbar itself.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTarget | [Canvas](#type-canvas) | true | — | target canvas to be scrolled |

### Groups

- scroll

---
