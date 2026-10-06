# Layout Documentation

[← Back to API Index](../reference.md)

---

## Class: Layout

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Arranges a set of "member" Canvases in horizontal or vertical stacks, applying a layout policy to determine member heights and widths.

A Layout manages a set of "member" Canvases provided as [Layout.members](#attr-layoutmembers). Layouts can have both "members", whose position and size are managed by the Layout, and normal Canvas children, which manage their own position and size.

Rather than using the Layout class directly, use the [HLayout](../reference.md#class-hlayout), [VLayout](../reference.md#class-vlayout), [HStack](../reference.md#class-hstack) and [VStack](../reference.md#class-vstack) classes, which are subclasses of Layout preconfigured for horizontal or vertical stacking, with the "fill" (VLayout) or "none" (VStack) [policies](../reference_2.md#type-layoutpolicy) already set.

Layouts and Stacks may be nested to create arbitrarily complex layouts.

Since Layouts can be either horizontally or vertically oriented, throughout the documentation of Layout and it's subclasses, the term "length" refers to the axis of stacking, and the term "breadth" refers to the other axis. Hence, "length" means height in the context of a VLayout or VStack, but means width in the context of an HLayout or HStack.

To show a resizer bar after (to the right or bottom of) a layout member, set [showResizeBar](Canvas.md#attr-canvasshowresizebar) to true on that member component (not on the HLayout or VLayout). Resizer bars override [membersMargin](#attr-layoutmembersmargin) spacing.

Like other Canvas subclasses, Layout and Stack components may have % width and height values. To create a dynamically-resizing layout that occupies the entire page (or entire parent component), set width and height to "100%".

### See Also

- [LayoutPolicy](../reference_2.md#type-layoutpolicy)
- [VLayout](../reference.md#class-vlayout)
- [HLayout](../reference.md#class-hlayout)
- [VStack](../reference.md#class-vstack)
- [HStack](../reference.md#class-hstack)
- [LayoutSpacer](../reference.md#class-layoutspacer)

---
## ClassAttr: Layout.FILL

### Description
A declared value of the enum type [LayoutPolicy](../reference_2.md#type-layoutpolicy).

**Flags**: R

---
## ClassAttr: Layout.NONE

### Description
A declared value of the enum type [LayoutPolicy](../reference_2.md#type-layoutpolicy).

**Flags**: R

---
## ClassAttr: Layout.VERTICAL

### Description
A declared value of the enum type [Orientation](../reference_2.md#type-orientation).

**Flags**: R

---
## ClassAttr: Layout.HORIZONTAL

### Description
A declared value of the enum type [Orientation](../reference_2.md#type-orientation).

**Flags**: R

---
## Attr: Layout.managePercentBreadth

### Description
If set, a Layout with breadthPolicy:"fill" will specially interpret a percentage breadth on a member as a percentage of available space excluding the [Layout.layoutMargin](#attr-layoutlayoutmargin). If false, percentages work exactly as for a non-member, with layoutMargins, if any, ignored.

**Flags**: IR

---
## Attr: Layout.members

### Description
An array of canvases that will be contained within this layout. You can set the following properties on these canvases (in addition to the standard component properties):

*   [layoutAlign](Canvas.md#attr-canvaslayoutalign) -- specifies the member's alignment along the breadth axis; valid values are "top", "center" and "bottom" for a horizontal layout and "left", "center" and "right" for a vertical layout (see [Layout.defaultLayoutAlign](#attr-layoutdefaultlayoutalign) for default implementation.)
*   [showResizeBar](Canvas.md#attr-canvasshowresizebar) -- set to true to show a resize bar (default is false)

Height and width settings found on members are interpreted by the Layout according to the [layout policy](#attr-layoutvpolicy).

Note that it is valid to have null slots in the provided `members` Array, and the Layout will ignore those slots. This can be useful to keep code compact, for example, when constructing the `members` Array, you might use an expression that either returns a component or null depending on whether the component should be present. If the expression returns null, the null slot will be ignored by the Layout.

**Flags**: IRW

---
## Attr: Layout.paddingAsLayoutMargin

### Description
If this widget has padding specified (as [this.padding](Canvas.md#attr-canvaspadding) or in the CSS style applied to this layout), should it show up as space outside the members, similar to layoutMargin?

If this setting is false, padding will not affect member positioning (as CSS padding normally does not affect absolutely positioned children). Leaving this setting true allows a designer to more effectively control layout purely from CSS.

Note that [Layout.layoutMargin](#attr-layoutlayoutmargin) if specified, takes precedence over this value.

### Groups

- layoutMargin

**Flags**: IRWA

---
## Attr: Layout.minMemberLength

### Description
Minimum size, in pixels, below which flexible-sized members should never be shrunk, even if this requires the Layout to overflow. Note that this property only applies along the _length_ axis of the Layout, and has no affect on _breadth_.

Does not apply to members given a fixed size in pixels - such members will never be shrunk below their specified size in general.

### Groups

- layoutPolicy

### See Also

- [Canvas.minWidth](Canvas.md#attr-canvasminwidth)

**Flags**: IRW

---
## Attr: Layout.enforcePolicy

### Description
Whether the layout policy is continuously enforced as new members are added or removed and as members are resized.

This setting implies that any member that resizes larger, or any added member, will take space from other members in order to allow the overall layout to stay the same size.

### Groups

- layoutPolicy

**Flags**: IRWA

---
## Attr: Layout.layoutRightMargin

### Description
Space outside of all members, on the right-hand side. Defaults to [Layout.layoutMargin](#attr-layoutlayoutmargin).

Requires a manual call to `setLayoutMargin()` if changed on the fly.

### Groups

- layoutMargin

**Flags**: IRW

---
## Attr: Layout.locateMembersBy

### Description
Part of the [automatedTesting](../kb_topics/automatedTesting.md#kb-topic-automated-testing) system, strategy to use when generated locators for members from within this Layout's members array.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Layout.membersMargin

### Description
Space between each member of the layout.

Requires a manual call to `reflow()` if changed on the fly.

### Groups

- layoutMargin

**Flags**: IRW

---
## Attr: Layout.stackZIndex

### Description
For use in conjunction with [Layout.memberOverlap](#attr-layoutmemberoverlap), controls the z-stacking order of members.

If set to "lastOnTop", members stack from the first member at bottom to the last member at top. If set to "firstOnTop", members stack from the last member at bottom to the first member at top.

**Flags**: IR

---
## Attr: Layout.placeHolderDefaults

### Description
If [this.showDragPlaceHolder](#attr-layoutshowdragplaceholder) is true, this defaults object determines the default appearance of the placeholder displayed when the user drags a widget out of this layout.  
Default value for this property sets the placeholder [styleName](Canvas.md#attr-canvasstylename) to `"layoutPlaceHolder"`  
To modify this object, use [Class.changeDefaults](Class.md#classmethod-classchangedefaults)

### Groups

- dragdrop

**Flags**: IR

---
## Attr: Layout.resizeBarSize

### Description
Thickness of the resizeBar in pixels.

**Flags**: AIRW

---
## Attr: Layout.memberOverlap

### Description
Number of pixels by which each member should overlap the preceding member, used for creating an "stack of cards" appearance for the members of a Layout.

`memberOverlap` can be used in conjunction with [Layout.stackZIndex](#attr-layoutstackzindex) to create a particular visual stacking order.

Note that overlap of individual members can be accomplished with a negative setting for [Canvas.extraSpace](Canvas.md#attr-canvasextraspace).

### Groups

- layoutMember

**Flags**: IR

---
## Attr: Layout.defaultResizeBars

### Description
Policy for whether resize bars are shown on members by default. Note that this setting changes the effect of [Canvas.showResizeBar](Canvas.md#attr-canvasshowresizebar) for members of this layout.

### See Also

- [Canvas.showResizeBar](Canvas.md#attr-canvasshowresizebar)

**Flags**: IRW

---
## Attr: Layout.vPolicy

### Description
Sizing policy applied to members on vertical axis

### Groups

- layoutPolicy

**Flags**: IRWA

---
## Attr: Layout.locateMembersType

### Description
[LocatorTypeStrategy](../reference.md#type-locatortypestrategy) to use when finding members within this layout.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Layout.leaveScrollbarGap

### Description
Whether to leave a gap for a vertical scrollbar even when one is not actually present.

This setting avoids the layout resizing all members when the vertical scrollbar is introduced or removed, which can avoid unnecessary screen shifting and improve performance.

**Flags**: IR

---
## Attr: Layout.vertical

### Description
Should this layout appear with members stacked vertically or horizontally. Defaults to `false` if unspecified.

### Groups

- layoutPolicy

**Flags**: IRW

---
## Attr: Layout.resizeBarClass

### Description
Default class to use for creating [resizeBars](#attr-layoutresizebar). This may be overridden by `resizeBarConstructor`.

Classes that are valid by default are [Splitbar](Splitbar.md#class-splitbar), [ImgSplitbar](ImgSplitbar.md#class-imgsplitbar), and [Snapbar](Snapbar.md#class-snapbar).

### See Also

- [Splitbar](Splitbar.md#class-splitbar)
- [ImgSplitbar](ImgSplitbar.md#class-imgsplitbar)

**Flags**: AIRW

---
## Attr: Layout.minBreadthMember

### Description
Set this property to cause the layout to assign the breadths of other members as if the available breadth is actually wide enough to accommodate the `minBreadthMember` (even though the Layout might _not_ actually be that wide, and may overflow its assigned size along the breadth axis due to the breadth of the `minBreadthMember`.

Without this property set, members of a layout aren't ever expanded in breadth (by the layout) to fit an overflow of the layout along the breadth axis. Setting this property will make sure all members (other than the one specified) get expanded to fill the full visual breadth of the layout (assuming they are configured to use 100% layout breadth).

### See Also

- [LayoutPolicy](../reference_2.md#type-layoutpolicy)

**Flags**: IRWA

---
## Attr: Layout.layoutTopMargin

### Description
Space outside of all members, on the top side. Defaults to [Layout.layoutMargin](#attr-layoutlayoutmargin).

Requires a manual call to `setLayoutMargin()` if changed on the fly.

### Groups

- layoutMargin

**Flags**: IRW

---
## Attr: Layout.animateMembers

### Description
If true when members are added / removed, they should be animated as they are shown or hidden in position

### Groups

- animation

**Flags**: IRW

---
## Attr: Layout.align

### Description
Alignment of all members in this Layout on the length axis (vertical for a VLayout, horizontal for an HLayout). Defaults to "top" for vertical Layouts, and "left" for horizontal Layouts.

Horizontal layouts should only be set to [Alignment](../reference_2.md#type-alignment), and vertical layouts to [VerticalAlignment](../reference.md#type-verticalalignment), otherwise they will be considered invalid values, and assigning an invalid value here will log a warning to the Developer Console.

For alignment on the breadth axis, see [Layout.defaultLayoutAlign](#attr-layoutdefaultlayoutalign) and [Canvas.layoutAlign](Canvas.md#attr-canvaslayoutalign).

When attempting to center components be sure that you have set a specific size on the component(s) involved. If components fill all available space in the layout, centering looks the same as not centering.

Similarly, if a component has no visible boundary (like a border), it can appear similar to when it's not centered if the component is larger than you expect - use the Watch tab in the Developer Console to see the component's extents visually.

### Groups

- layoutPolicy

**Flags**: IRW

---
## Attr: Layout.layoutStartMargin

### Description
Equivalent to [Layout.layoutLeftMargin](#attr-layoutlayoutleftmargin) for a horizontal layout, or [Layout.layoutTopMargin](#attr-layoutlayouttopmargin) for a vertical layout.

If both `layoutStartMargin` and the more specific properties (top/left margin) are both set, the more specific properties win.

**Flags**: IRW

---
## Attr: Layout.defaultLayoutAlign

### Description
Specifies the default alignment for layout members on the breadth axis (horizontal axis for a VLayout, vertical axis for an HLayout). Can be overridden on a per-member basis by setting [Canvas.layoutAlign](Canvas.md#attr-canvaslayoutalign).

If unset, default member layout alignment will be "top" for a horizontal layout, and "left" for a vertical layout, or "right" if in [RTL](Page.md#classmethod-pageisrtl) mode.

When attempting to center components be sure that you have set a specific size on the component(s) involved. If components fill all available space in the layout, centering looks the same as not centering.

Similarly, if a component has no visible boundary (like a border), it can appear similar to when it's not centered if the component is larger than you expect - use the Watch tab in the Developer Console to see the component's extents visually.

### Groups

- layoutMember
- layoutPolicy

### See Also

- [Layout.overflow](#attr-layoutoverflow)

**Flags**: IRW

---
## Attr: Layout.dropLineThickness

### Description
Thickness, in pixels of the dropLine shown during drag and drop when [Layout.canDropComponents](#attr-layoutcandropcomponents) is set to `true`. See the discussion in [Layout](#class-layout) for more info.

### Groups

- dragdrop

### See Also

- [Layout](#class-layout)

**Flags**: IRA

---
## Attr: Layout.dropLine

### Description
Line showed to mark the drop position when components are being dragged onto this Layout. A simple Canvas typically styled via CSS. The default dropLine.styleName is "layoutDropLine".

**Flags**: R

---
## Attr: Layout.layoutMargin

### Description
Space outside of all members. This attribute, along with [Layout.layoutLeftMargin](#attr-layoutlayoutleftmargin) and related properties do not have a true setter method. It may be assigned directly at runtime. After setting the property, [Layout.setLayoutMargin](#method-layoutsetlayoutmargin) may be called with no arguments to reflow the layout.

### Groups

- layoutMargin

### See Also

- [Layout.layoutLeftMargin](#attr-layoutlayoutleftmargin)
- [Layout.layoutRightMargin](#attr-layoutlayoutrightmargin)
- [Layout.layoutBottomMargin](#attr-layoutlayoutbottommargin)
- [Layout.layoutTopMargin](#attr-layoutlayouttopmargin)
- [Layout.paddingAsLayoutMargin](#attr-layoutpaddingaslayoutmargin)

**Flags**: IRW

---
## Attr: Layout.resizeBar

### Description
A MultiAutoChild created to resize members of this `Layout`.

A resize bar will be created for any member of this `Layout` that has [showResizeBar](Canvas.md#attr-canvasshowresizebar) set to `true`. Resize bars will be instances of the class specified by [Layout.resizeBarClass](#attr-layoutresizebarclass) by default, and will automatically be sized to the member's breadth, and to the thickness specified by [Layout.resizeBarSize](#attr-layoutresizebarsize).

To customize the appearance or behavior of resizeBars within some layout a custom resize bar class can be created by subclassing [Splitbar](Splitbar.md#class-splitbar) or [ImgSplitbar](ImgSplitbar.md#class-imgsplitbar) and setting [Layout.resizeBarClass](#attr-layoutresizebarclass) or `resizeBarConstructor` to this custom class. Alternatively, `resizeBarProperties` may be specified. See [autoChildUsage](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) for more information.

The built-in `Splitbar` class supports drag resizing of its target member, and clicking on the bar with a mouse to collapse/uncollapse the target member.

**Flags**: A

---
## Attr: Layout.animateMemberTime

### Description
If specified this is the duration of show/hide animations when members are being shown or hidden due to being added / removed from this layout.

### Groups

- animation

**Flags**: IRWA

---
## Attr: Layout.hPolicy

### Description
Sizing policy applied to members on horizontal axis

### Groups

- layoutPolicy

**Flags**: IRWA

---
## Attr: Layout.placeHolderProperties

### Description
If [this.showDragPlaceHolder](#attr-layoutshowdragplaceholder) is true, this properties object can be used to customize the appearance of the placeholder displayed when the user drags a widget out of this layout.

### Groups

- dragdrop

**Flags**: IR

---
## Attr: Layout.showDragPlaceHolder

### Description
If set to true, when a member is dragged out of layout, a visible placeholder canvas will be displayed in place of the dragged widget for the duration of the drag and drop interaction.

### Groups

- dragdrop

**Flags**: IRW

---
## Attr: Layout.overflow

### Description
A Layout may overflow if it has one or more members with a fixed width or height, or that themselves overflow. For details on member sizing see [LayoutPolicy](../reference_2.md#type-layoutpolicy).

Note that for overflow: "auto", "scroll", or "visible", members exceeding the Layout's specified breadth but falling short of its overflow breadth will keep the alignment set via [Layout.defaultLayoutAlign](#attr-layoutdefaultlayoutalign) or [Canvas.layoutAlign](Canvas.md#attr-canvaslayoutalign).

### Groups

- layoutPolicy

### See Also

- [Canvas.overflow](Canvas.md#attr-canvasoverflow)
- [Layout.minBreadthMember](#attr-layoutminbreadthmember)

**Flags**: IRW

---
## Attr: Layout.layoutBottomMargin

### Description
Space outside of all members, on the bottom side. Defaults to [Layout.layoutMargin](#attr-layoutlayoutmargin).

Requires a manual call to `setLayoutMargin()` if changed on the fly.

### Groups

- layoutMargin

**Flags**: IRW

---
## Attr: Layout.showDropLines

### Description
Controls whether to show a drop-indicator during a drag and drop operation. Set to false if you either don't want to show drop-lines, or plan to create your own.

### Groups

- dragdrop

**Flags**: IRW

---
## Attr: Layout.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Layout.layoutEndMargin

### Description
Equivalent to [Layout.layoutRightMargin](#attr-layoutlayoutrightmargin) for a horizontal layout, or [Layout.layoutBottomMargin](#attr-layoutlayoutbottommargin) for a vertical layout.

If both `layoutEndMargin` and the more specific properties (right/bottom margin) are both set, the more specific properties win.

**Flags**: IRW

---
## Attr: Layout.layoutLeftMargin

### Description
Space outside of all members, on the left-hand side. Defaults to [Layout.layoutMargin](#attr-layoutlayoutmargin).

Requires a manual call to `setLayoutMargin()` if changed on the fly.

### Groups

- layoutMargin

**Flags**: IRW

---
## Attr: Layout.minMemberSize

### Description
See [Layout.minMemberLength](#attr-layoutminmemberlength).

### Groups

- layoutPolicy

**Deprecated**

**Flags**: IRW

---
## Attr: Layout.canDropComponents

### Description
Layouts provide a default implementation of a drag and drop interaction. If you set [canAcceptDrop](Canvas.md#attr-canvascanacceptdrop):true and `canDropComponents:true` on a Layout, when a droppable Canvas ([canDrop:true](Canvas.md#attr-canvascandrop) is dragged over the layout, it will show a dropLine (a simple insertion line) at the drop location.

When the drop occurs, [Layout.getDropComponent](#method-layoutgetdropcomponent) is invoked to determine which component should be added to the layout as a member at the location calculated by [Layout.getDropPosition](#method-layoutgetdropposition). By default this method will return the current drag target. This default behavior allows existing members to be reordered or external components that have [Canvas.canDragReposition](Canvas.md#attr-canvascandragreposition) (or [Canvas.canDrag](Canvas.md#attr-canvascandrag)) and [Canvas.canDrop](Canvas.md#attr-canvascandrop) set to `true` to be added to the Layout.

You can control the thickness of the dropLine via [Layout.dropLineThickness](#attr-layoutdroplinethickness) and you can customize the style using css styling in the skin file (look for .layoutDropLine in skin\_styles.css for your skin).

If you want to dynamically create a component to be added to the Layout in response to a drop event you can override [Layout.getDropComponent](#method-layoutgetdropcomponent), or for entirely custom behavior override the [drop event handler](#method-layoutdrop) as follows:

```
 isc.VLayout.create({
   ...various layout properties...
   canDropComponents: true,
   drop : function () {
     // create the new component 
     var newMember = isc.Canvas.create(); 
     // add to the layout at the current drop position 
     // (the dropLine will be showing here)
     this.addMember(newMember, this.getDropPosition());  
     // hide the dropLine that was automatically shown 
     // by builtin SmartClient methods
     this.hideDropLine();
   }
 });
 
```
If you want to completely suppress the builtin drag and drop logic, but still receive drag and drop events for your own custom implementation, set [Canvas.canAcceptDrop](Canvas.md#attr-canvascanacceptdrop) to `true` and `canDropComponents` to `false` on your Layout.

### Groups

- dragdrop

**Flags**: IRA

---
## Attr: Layout.reverseOrder

### Description
Reverse the order of stacking for this Layout, so that the last member is shown first.

Requires a manual call to `reflow()` if changed on the fly.

In RTL mode, for horizontal Layouts the value of this flag will be flipped during initialization.

### Groups

- layoutPolicy

**Flags**: IRW

---
## Attr: Layout.orientation

### Description
Orientation of this layout.

### Groups

- layoutPolicy

**Deprecated**

**Flags**: AIRW

---
## Method: Layout.reflow

### Description
Layout members according to current settings.

Members will reflow automatically when the layout is resized, members resize, the list of members changes or members change visibility. It is only necessary to manually call `reflow()` after changing settings on the layout, for example, `layout.reverseOrder`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | true | — | reason reflow() had to be called (appear in logs if enabled) |

**Flags**: A

---
## Method: Layout.removeMember

### Description
Removes the specified member from the layout. If it has a resize bar, the bar will be destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | the canvas to be removed from the layout |

---
## Method: Layout.removeMembers

### Description
Removes the specified members from the layout. If any of the removed members have resize bars, the bars will be destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| members | [Array of Canvas](#type-array-of-canvas)|[Canvas](#type-canvas) | false | — | array of members to be removed, or single member |

---
## Method: Layout.setLayoutMargin

### Description
Method to force a reflow of the layout after directly assigning a value to any of the layout\*Margin properties. Takes no arguments.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMargin | [Integer](../reference_2.md#type-integer) | true | — | optional new setting for layout.layoutMargin. Regardless of whether a new layout margin is passed, the layout reflows according to the current settings for layoutStartMargin et al |

### Groups

- layoutMargin

---
## Method: Layout.getChildTabPosition

### Description
Layouts ensure children are ordered in the tab-sequence with members being reachable first (in member order), then any non-member children.

As with [Canvas.getChildTabPosition](Canvas.md#method-canvasgetchildtabposition) if [Canvas.setRelativeTabPosition](Canvas.md#method-canvassetrelativetabposition) was called explicitly called for some child, it will be respected over member order.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [Canvas](#type-canvas) | false | — | The child for which the tab position should be returned |

### Returns

`[Integer](../reference_2.md#type-integer)` — tab position of the child within this layout.

---
## Method: Layout.getMemberNumber

### Description
Given a member Canvas or member [ID](Canvas.md#attr-canvasid) or [name](Canvas.md#attr-canvasname), return the index of that member within this layout's members array. If passed a number, just returns it.

Note that if more than one member has the same `name`, passing in a `name` has an undefined result.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| memberID | [String](#type-string)|[Canvas](#type-canvas)|[int](../reference.md#type-int) | false | — | identifier for the required member |

### Returns

`[int](../reference.md#type-int)` — index of the member canvas (or -1 if not found)

### See Also

- [Layout.getMember](#method-layoutgetmember)

---
## Method: Layout.setVisibleMember

### Description
Hide all other members and make the single parameter member visible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | member to show |

---
## Method: Layout.reorderMembers

### Description
Move a range of members to a new position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | beginning of range of members to move |
| end | [number](#type-number) | false | — | end of range of members to move, non-inclusive |
| newPosition | [number](#type-number) | false | — | new position to move the members to |

---
## Method: Layout.hasMember

### Description
Returns true if the layout includes the specified canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | the canvas to check for |

### Returns

`[Boolean](#type-boolean)` — true if the layout includes the specified canvas

---
## Method: Layout.getMemberSizes

### Description
—

### Returns

`[Array](#type-array)` — array of member sizes

---
## Method: Layout.drop

### Description
Layouts have built-in handling of component drag and drop. See the discussion in [Layout.canDropComponents](#attr-layoutcandropcomponents) on how it works. If you override this builtin implementation of drop() and you're using the built-in dropLine via [Layout.canDropComponents](#attr-layoutcandropcomponents):true, be sure to call [Layout.hideDropLine](#method-layouthidedropline) to hide the dropLine after doing your custom drop() handling.

### Returns

`[boolean](../reference.md#type-boolean)` — Returning false will cancel the drop entirely

**Flags**: A

---
## Method: Layout.getMemberOffset

### Description
Override point for changing the offset on the breadth axis for members, that is, the offset relative to the left edge for a vertical layout, or the offset relative to the top edge for a horizontal layout.

The method is passed the default offset that would be used for the member if getMemberOffset() were not implemented. This default offset already takes into account [Layout.layoutMargin](#attr-layoutlayoutmargin), as well as the [alignment on the breadth axis](#attr-layoutdefaultlayoutalign), which is also passed to getMemberOffset().

This method is an override point only; it does not exist by default and cannot be called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | Component to be positioned |
| defaultOffset | [Number](#type-number) | false | — | Value of the currently calculated member offset. If this value is returned unchanged the layout will have its default behavior |
| alignment | [String](#type-string) | false | — | alignment of the enclosing layout, on the breadth axis |

### Groups

- layoutMember

**Flags**: A

---
## Method: Layout.getMember

### Description
Given a numerical index or a member [name](Canvas.md#attr-canvasname) or member [ID](Canvas.md#attr-canvasid), return a pointer to the appropriate member. If passed a member Canvas, just returns it.

Note that if more than one member has the same `name`, passing in a `name` has an undefined result.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| memberID | [String](#type-string)|[int](../reference.md#type-int)|[Canvas](#type-canvas) | false | — | identifier for the required member |

### Returns

`[Canvas](#type-canvas)` — member widget

### See Also

- [Layout.getMemberNumber](#method-layoutgetmembernumber)

---
## Method: Layout.showMember

### Description
Show the specified member, firing the specified callback when the show is complete.

Members can always be directly shown via `member.show()`, but if [animation](#attr-layoutanimatemembers) is enabled, animation will only occur if showMember() is called to show the member.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | Member to show |
| callback | [Function](#type-function) | true | — | action to fire when the member has been shown |

---
## Method: Layout.getMembersLength

### Description
Convenience method to return the number of members this Layout has

### Returns

`[Integer](../reference_2.md#type-integer)` — the number of members this Layout has

---
## Method: Layout.reorderMember

### Description
Shift a member of the layout to a new position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| memberNum | [number](#type-number) | false | — | current position of the member to move to a new position |
| newPosition | [number](#type-number) | false | — | new position to move the member to |

---
## Method: Layout.hideMember

### Description
Hide the specified member, firing the specified callback when the hide is complete.

Members can always be directly hidden via `member.hide()`, but if [animation](#attr-layoutanimatemembers) is enabled, animation will only occur if hideMember() is called to hide the member.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | Member to hide |
| callback | [Function](#type-function) | true | — | callback to fire when the member is hidden. |

---
## Method: Layout.getDropPosition

### Description
Get the position a new member would be dropped. This drop position switches in the middle of each member, and both edges (before beginning, after end) are legal drop positions

Use this method to obtain the drop position for e.g. a custom drop handler.

### Returns

`[int](../reference.md#type-int)` — the position a new member would be dropped

**Flags**: A

---
## Method: Layout.getDropComponent

### Description
When [Layout.canDropComponents](#attr-layoutcandropcomponents) is true, this method will be called when a component is dropped onto the layout to determine what component to add as a new layout member.

By default, the actual component being dragged (isc.EventHandler.getDragTarget()) will be added to the layout. For a different behavior, such as wrapping dropped components in Windows, or creating components on the fly from dropped data, override this method.

You can also return null to cancel the drop.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dragTarget | [Canvas](#type-canvas) | false | — | current drag target |
| dropPosition | [int](../reference.md#type-int) | false | — | index of the drop in the list of current members |

### Returns

`[Canvas](#type-canvas)` — the component to add to the layout, or null to cancel the drop

---
## Method: Layout.membersChanged

### Description
Fires once at initialization if the layout has any initial members, and then fires whenever members are added, removed or reordered.

---
## Method: Layout.replaceMember

### Description
Replaces an existing member of the layout with a different widget. The new member will be assigned the width and height of the existing member (including sizes configured via end user resize), so no reflow will occur unless the new component has visible overflow and it differs from that of the widget it replaced.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldMember | [Canvas](#type-canvas) | false | — | an existing member of the layout to be replaced |
| newMember | [Canvas](#type-canvas) | false | — | a different widget that should replace `oldMember` |

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

---
## Method: Layout.setMembers

### Description
Display a new set of members in this layout. Equivalent to calling removeMembers() then addMembers(). Note that the new members may include members already present, in which case they will be reordered / integrated with any other new members passed into this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| members | [Array of Canvas](#type-array-of-canvas) | false | — | — |

---
## Method: Layout.reflowNow

### Description
Layout members according to current settings, immediately.  
Generally, when changes occur that require a layout to reflow (such as members being shown or hidden), the Layout will reflow only after a delay, so that multiple changes cause only one reflow. To remove this delay for cases where it is not helpful, reflowNow() can be called.

**Flags**: A

---
## Method: Layout.revealChild

### Description
Reveals the child or member Canvas passed in by showing it if it is currently hidden

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [GlobalId](../reference.md#type-globalid)|[Canvas](#type-canvas) | false | — | the child Canvas to reveal, or its global ID |

---
## Method: Layout.addMember

### Description
Add a canvas to the layout, optionally at a specific position.

Depending on the layout policy, adding a new member may cause existing members to resize.

When adding a member to a drawn Layout, the layout will not immediately reflow, that is, the member will not immediately draw and existing members will not immediately resize. This is to allow multiple new members to be added and multiple manual resizes to take place without requiring layout members to redraw and resize multiple times.

To force an immediate reflow in order to, for example, find out what size a newly added member has been assigned, call [Layout.reflowNow](#method-layoutreflownow).

The `position` parameter specifies where the member (or members for [Layout.addMembers](#method-layoutaddmembers)) should be inserted within the existing members of this layout. You can think of this as the index of a gap between existing members. If `addMember()` is called with an existing member this may not be the same as the final index for the member after the method completes. If the member is being moved forwards, it will be removed and reinserted at the specified insertion position, meaning the final index will be `position-1`.

For example, if a layout has a member `_myMember_` at index `n` within the members array,  
  `layout.addMember(_myMember_, n+1);`  
would attempt to insert the member directly after itself (which is a no-op) and  
  `layout.addMember(_myMember_, n+2);`  
places the member after the component that currently follows it in the members array. This will ultimately put `myMember` at index `n+1`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMember | [Canvas](#type-canvas) | false | — | the canvas object to be added to the layout |
| position | [Integer](../reference_2.md#type-integer) | true | — | If passed, this specifies the insertion position between the existing members of the layout. If omitted, the canvas will be added at the last position |

### See Also

- [Layout.addMembers](#method-layoutaddmembers)

---
## Method: Layout.getMembers

### Description
Get the Array of members.

**NOTE**: the returned array should not be modified directly. Use [Layout.addMember](#method-layoutaddmember) / [Layout.removeMember](#method-layoutremovemember) to add or remove members from the Layout. Call [duplicate()](List.md#method-listduplicate) on the returned Array if you need a copy of the members array for some other purpose.

### Returns

`[Array of Canvas](#type-array-of-canvas)` — the Array of members

---
## Method: Layout.addMembers

### Description
Add one or more canvases to the layout, optionally at a specific position. See [Layout.addMember](#method-layoutaddmember) for details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMembers | [Array of Canvas](#type-array-of-canvas)|[Canvas](#type-canvas) | false | — | array of canvases to be added or single Canvas |
| position | [Integer](../reference_2.md#type-integer) | true | — | If passed, this specifies the insertion position between the existing members of the layout. If omitted, the canvas will be added at the last position |

---
## Method: Layout.hideDropLine

### Description
Calling this method hides the dropLine shown during a drag and drop interaction with a Layout that has [Layout.canDropComponents](#attr-layoutcandropcomponents) set to true. This method is only useful for custom implementations of [Layout.drop](#method-layoutdrop) as the default implementation calls this method automatically.

**Flags**: A

---
## Method: Layout.getMemberDefaultBreadth

### Description
Return the breadth for a member of this layout which either didn't specify a breadth or specified a percent breadth with [Layout.managePercentBreadth](#attr-layoutmanagepercentbreadth):true.

Called only for Layouts which have a [layout policy](../reference_2.md#type-layoutpolicy) for the breadth axis of "fill", since Layouts with a breadth policy of "none" leave all member breadths alone.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| member | [Canvas](#type-canvas) | false | — | Component to be sized |
| defaultBreadth | [Number](#type-number) | false | — | Value of the currently calculated member breadth. This may be returned verbatim or manipulated in this method. |

### Groups

- layoutMember

**Flags**: A

---
## Method: Layout.setAlign

### Description
Changes the [Layout.align](#attr-layoutalign) for this Layout.

Horizontal layouts should only be changed to [Alignment](../reference_2.md#type-alignment), and vertical layouts to [VerticalAlignment](../reference.md#type-verticalalignment), otherwise they will be considered invalid values, and assigning an invalid value here will log a warning to the Developer Console.

For alignment on the breadth axis, see [Layout.defaultLayoutAlign](#attr-layoutdefaultlayoutalign) and [Canvas.layoutAlign](Canvas.md#attr-canvaslayoutalign).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| align | [Alignment](../reference_2.md#type-alignment)|[VerticalAlignment](../reference.md#type-verticalalignment) | false | — | — |

---
## Method: Layout.layoutIsDirty

### Description
Returns whether there is a pending reflow of the members of the layout.

Modifying the set of members, resizing members or changing layout settings will cause a recalculation of member sizes to be scheduled. The recalculation is delayed so that it is not performed redundantly if multiple changes are made in a row.

To force immediate recalculation of new member sizes and resizing of members, call [Layout.reflowNow](#method-layoutreflownow).

### Returns

`[boolean](../reference.md#type-boolean)` — whether the layout is currently dirty

**Flags**: A

---
