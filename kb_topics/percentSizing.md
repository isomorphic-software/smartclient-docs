# Canvas Percentage sizing

[← Back to API Index](../main.md)

---

## KB Topic: Canvas Percentage sizing

### Description
Canvas [width](../classes/Canvas.md#attr-canvaswidth) and [height](../classes/Canvas.md#attr-canvasheight) may be set to a percentage value or `"*"` rather than an explicit pixel value. This indicates to the framework that these widgets should be sized dynamically.

Percentage sizes are resolved to pixel values as follows:

*   If a canvas has a specified [percentSource](../classes/Canvas.md#attr-canvaspercentsource), sizing will be a percentage of the size of that widget (see also [Canvas.percentBox](../classes/Canvas.md#attr-canvaspercentbox)).
*   Otherwise, if a canvas has a [master canvas](../classes/Canvas.md#method-canvasgetmastercanvas), and [snapTo](../classes/Canvas.md#attr-canvassnapto) is set for the widget, sizing will be a percentage of the size of that widget (see also [Canvas.percentBox](../classes/Canvas.md#attr-canvaspercentbox)).
*   Otherwise if this is a child of some other canvas, percentages will be based on the inner size of the [parent canvas](../classes/Canvas.md#method-canvasgetparentcanvas)'s viewport. This is the available space inside the parent, taking border, scrollbars etc into account.  
    If the parent has overflow set to "visible", percentage sizes are based on the inner _specified_ size of the parent rather than the overflowed size.
*   Otherwise, for top level widgets, sizing is calculated as a percentage of page size.

[Layouts](../classes/Layout.md#class-layout) may specially interpret percentage sizes on their children, and also allow "\*" as a size. See the Layout class documentation for more information.

**Minimums and maximums for dynamic sizing:**  
Note that if a [Canvas.maxWidth](../classes/Canvas.md#attr-canvasmaxwidth) or [Canvas.minWidth](../classes/Canvas.md#attr-canvasminwidth) are specified (or [Canvas.maxHeight](../classes/Canvas.md#attr-canvasmaxheight) / [Canvas.minHeight](../classes/Canvas.md#attr-canvasminheight) for heights), these properties act as explicit pixel limits on the canvas' size. For example, a canvas with [Canvas.maxWidth](../classes/Canvas.md#attr-canvasmaxwidth) set to `500`, and width specified as "100%" will not render larger than 500 pixels in width even if there is more space available in the parent canvas or percentSource.

**Percent sizing within _overflow:"visible"_ parents:**  
If a canvas is a [child](../classes/Canvas.md#attr-canvaschildren) of another canvas with [Canvas.overflow](../classes/Canvas.md#attr-canvasoverflow) set to "visible", percentage sizes are based on the specified size of the parent, not the drawn size. In other words - if the parent's content, or the size and position of some other child cause it to render larger than its specified size, a "100%"-sized child will not expand to fill the larger, rendered size of the parent.

The framework avoids sizing percent sized children to fit the _overflowed_ size of their parents, as the child itself contributes to the overflowed size of the parent. If a child both drives and is driven by its parent's overflowed size unintended behaviors become very likely.  
It becomes much more likely to see runaway sizing and infinite loops with this kind of pattern and, while a parent holding a child sized to its overflowed inner height or width could grow (for example, expanding its overflow to accommodate another, taller child), it would never dynamically reduce its overflow, as the percent sized child would always completely fill the drawn area.

Note that a developer could explicitly set the [Canvas.percentSource](../classes/Canvas.md#attr-canvaspercentsource) attribute of some canvas to its parent, but this isn't recommended for the reasons described above. If you are trying to make a canvas fit to the (overflowed) viewport of its parent, it is probably appropriate to instead match the size of the sibling causing it to overflow. This could be achieved by setting `percentSource` to that sibling and setting an appropriate percentBox value. You could also consider whether a [master/peer relationship](containment.md#kb-topic-component-containment-and-hierarchy) is appropriate.

Also note that the [Layout](../classes/Layout.md#class-layout) class supports expanding all members to match the drawn size of some [minimum breadth member](../classes/Layout.md#attr-layoutminbreadthmember).

Developers wishing to implement some other dynamic sizing paradigm for a component based on the drawn size of other component(s) can also add custom handling to the [resized notification](../classes/Canvas.md#method-canvasresized).

---
