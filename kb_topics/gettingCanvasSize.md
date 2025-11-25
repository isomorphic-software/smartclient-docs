# Determining the size of a drawn canvas

[← Back to API Index](../main.md)

---

## KB Topic: Determining the size of a drawn canvas

### Description
A canvas's size is determined by its specified [width](../classes/Canvas.md#attr-canvaswidth), [height](../classes/Canvas.md#attr-canvasheight) as well as its [overflow](../classes/Canvas.md#attr-canvasoverflow).

The following methods are available to retrieve the size of a canvas at runtime:

| [Canvas.getWidth](../classes/Canvas.md#method-canvasgetwidth), [Canvas.getHeight](../classes/Canvas.md#method-canvasgetheight) | Returns the specified size of the component in pixels. If height or width were specified as a [percentage value](percentSizing.md#kb-topic-canvas-percentage-sizing), this method will return the resolved absolute size. |
|---|---|
| [Canvas.getInnerWidth](../classes/Canvas.md#method-canvasgetinnerwidth), [Canvas.getInnerHeight](../classes/Canvas.md#method-canvasgetinnerheight) | Returns the amount of space available for absolutely positioned child widget(s) or absolutely positioned HTML content, without introducing clipping, scrolling or overflow.This is the space within the viewport of the widget (including padding, but excluding margins, borders or scrollbars) rendered at its specified size. |
| [Canvas.getInnerContentWidth](../classes/Canvas.md#method-canvasgetinnercontentwidth), [Canvas.getInnerContentHeight](../classes/Canvas.md#method-canvasgetinnercontentheight) | Returns the amount of space available for relatively positioned child widget(s) or inline positioned HTML content, without introducing clipping, scrolling or overflow.This is the space within the viewport of the widget (not including padding, excluding margins, borders or scrollbars) rendered at its specified size. |
| [Canvas.getVisibleWidth](../classes/Canvas.md#method-canvasgetvisiblewidth), [Canvas.getVisibleHeight](../classes/Canvas.md#method-canvasgetvisibleheight) | Returns the drawn size of the component in pixels, (including border, margin and scrollbars). If a widget is undrawn or has [overflow](../classes/Canvas.md#attr-canvasoverflow) set to something other than "visible", this will match the value returned by [Canvas.getWidth](../classes/Canvas.md#method-canvasgetwidth) or [Canvas.getHeight](../classes/Canvas.md#method-canvasgetheight). For an overflow:"visible" canvas this value will be greater than the specified size if the size of children or content exceeds the available space. |
| [Canvas.getViewportWidth](../classes/Canvas.md#method-canvasgetviewportwidth), [Canvas.getViewportHeight](../classes/Canvas.md#method-canvasgetviewportheight) | Returns the drawn size of the component's viewport in pixels. This is the same value as [Canvas.getVisibleWidth](../classes/Canvas.md#method-canvasgetvisiblewidth) / [Canvas.getVisibleWidth](../classes/Canvas.md#method-canvasgetvisiblewidth), less any border, margin or scrollbars |
| [Canvas.getScrollWidth](../classes/Canvas.md#method-canvasgetscrollwidth), [Canvas.getScrollHeight](../classes/Canvas.md#method-canvasgetscrollheight) | Returns the scrollable size of the widget's content, including children.For components with [Canvas.overflow](../classes/Canvas.md#attr-canvasoverflow) set to something other than "visible", this value may exceed the [drawn size](../classes/Canvas.md#method-canvasgetvisiblewidth) of the canvas. See also [Canvas.getScrollLeft](../classes/Canvas.md#method-canvasgetscrollleft), [Canvas.getScrollTop](../classes/Canvas.md#method-canvasgetscrolltop). |

---
