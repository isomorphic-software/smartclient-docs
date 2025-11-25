# PointerSettings Documentation

[← Back to API Index](../main.md)

---

## Attr: PointerSettings.showShadow

### Description
By default, the pointer will show the same shadow as its parent canvas. Set `showShadow` to false to render the pointer without a shadow.

**Flags**: IR

---
## Attr: PointerSettings.cornerOffset

### Description
Specifies the amount of offset in pixels from the corner to position the pointer when [PointerSettings.snapTo](#attr-pointersettingssnapto) is TL, TR, BL or BR. This is useful for a canvas with a rounded corner.

**Flags**: IR

---
## Attr: PointerSettings.snapOffsetLeft

### Description
If [snapTo](#attr-pointersettingssnapto) is defined, this property can be used to specify an offset in px or percentage for the left coordinate of the pointer.

For example if `snapTo` is specified as `"L"` and `snapOffsetLeft` is set to 6, the pointer will be rendered 6px inside the left edge of the window. Alternatively if `snapTo` was set to `"R"`, a `snapOffsetLeft` value of -6 would cause the pointer to be rendered 6px inside the right edge of the window.

### Groups

- snapPositioning

### See Also

- [PointerSettings.snapTo](#attr-pointersettingssnapto)

**Flags**: IR

---
## Attr: PointerSettings.color

### Description
By default, the pointer will assume the same color as its parent canvas. Set this attribute to enforce a custom color for the pointer.

**Flags**: IR

---
## Attr: PointerSettings.targetSnapTo

### Description
Specifies the position of the pointer into the target when [showing](Canvas.md#attr-canvasshowpointer). Accepts the same values as [PointerSettings.snapTo](#attr-pointersettingssnapto).

If not specified the center location on the appropriate edge is chosen to match up with the [PointerSettings.snapTo](#attr-pointersettingssnapto) value.

### Groups

- snapGridDragging

**Flags**: IR

---
## Attr: PointerSettings.targetOffsetTop

### Description
If [targetSnapTo](#attr-pointersettingstargetsnapto) is defined, this property can be used to specify an offset in px or percentage for the top coordinate of the pointer.

For example if `targetSnapTo` is specified as `"T"` and `targetOffsetTop` is set to 6, the pointer will be rendered 6px below the top edge of the pointer target canvas. Alternatively if `targetSnapTo` was set to `"B"`, a `targetOffsetTop` value of -6 would cause the pointer to be rendered 6px inside the bottom edge of the pointer target canvas.

Note that [PointerSettings.targetOffsetInto](#attr-pointersettingstargetoffsetinto) is likely more suitable for simple customizations.

### See Also

- [PointerSettings.targetSnapTo](#attr-pointersettingstargetsnapto)
- [PointerSettings.targetOffsetInto](#attr-pointersettingstargetoffsetinto)

**Flags**: IR

---
## Attr: PointerSettings.snapOffsetTop

### Description
If [snapTo](#attr-pointersettingssnapto) is defined, this property can be used to specify an offset in px or percentage for the top coordinate of the pointer.

For example if `snapTo` is specified as `"T"` and `snapOffsetTop` is set to 6, the pointer will be rendered 6px below the top edge of the window. Alternatively if `snapTo` was set to `"B"`, a `snapOffsetTop` value of -6 would cause the pointer to be rendered 6px inside the bottom edge of the window.

### Groups

- snapPositioning

### See Also

- [PointerSettings.snapTo](#attr-pointersettingssnapto)

**Flags**: IR

---
## Attr: PointerSettings.snapTo

### Description
Specifies the position of the pointer when [showing](Canvas.md#attr-canvasshowpointer). Accepts similar values as [Canvas.snapTo](Canvas.md#attr-canvassnapto).

Possible basic values: TL, TR, LT, LB, RT, RB, BL, BR, R, L, B, T where B=Bottom, T=Top, L=Left, R=right. The first letter indicates the edge and the second optional letter indicates the placement along the edge.

In addition to the basic values above, two different basic values can be combined with a separating slash (/) to position the pointer between the two locations giving more precise control. For example, `BL/L` positions the pointer along the bottom edge halfway between the bottom-left and the bottom-center.

If [Canvas.showPointer](Canvas.md#attr-canvasshowpointer) is enabled and a [Canvas.pointerTarget](Canvas.md#attr-canvaspointertarget) is specified but `snapTo` is null, a reasonable location is calculated based on the location of the `pointerTarget`.

### Groups

- snapPositioning

**Flags**: IR

---
## Attr: PointerSettings.targetOffsetInto

### Description
If [targetSnapTo](#attr-pointersettingstargetsnapto) is defined, this property can be used to specify an offset in px or percentage for the coordinate of the pointer _into_ the [Canvas.pointerTarget](Canvas.md#attr-canvaspointertarget).

While [PointerSettings.targetOffsetLeft](#attr-pointersettingstargetoffsetleft) and [PointerSettings.targetOffsetTop](#attr-pointersettingstargetoffsettop) can be used to fine tune the pointer's target position the user must be aware of the orientation of the pointer. Instead, this property will be applied to the correct offset so that the pointer points inside (or outside if negative) the target.

For example if `targetSnapTo` is specified as `"L"` and `targetOffsetInto` is set to 6, the pointer will be rendered 6px inside the left edge of the position target.

### See Also

- [PointerSettings.targetSnapTo](#attr-pointersettingstargetsnapto)

**Flags**: IR

---
## Attr: PointerSettings.targetOffsetLeft

### Description
If [targetSnapTo](#attr-pointersettingstargetsnapto) is defined, this property can be used to specify an offset in px or percentage for the left coordinate of the pointer.

For example if `targetSnapTo` is specified as `"L"` and `targetOffsetLeft` is set to 6, the pointer will be rendered 6px inside the left edge of the pointer target canvas. Alternatively if `targetSnapTo` was set to `"R"`, a `targetOffsetLeft` value of -6 would cause the pointer to be rendered 6px inside the right edge of the pointer target canvas.

Note that [PointerSettings.targetOffsetInto](#attr-pointersettingstargetoffsetinto) is likely more suitable for simple customizations.

### See Also

- [PointerSettings.targetSnapTo](#attr-pointersettingstargetsnapto)
- [PointerSettings.targetOffsetInto](#attr-pointersettingstargetoffsetinto)

**Flags**: IR

---
