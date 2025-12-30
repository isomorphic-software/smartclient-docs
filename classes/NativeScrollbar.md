# NativeScrollbar Documentation

[← Back to API Index](../reference.md)

---

## Class: NativeScrollbar

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
The NativeScrollbar widget will render in the browser as a native scrollbar, and has APIs allowing it to be applied to scroll content any another widget on the page. Essentially this behaves similarly to the [Scrollbar](Scrollbar.md#class-scrollbar) class but will be rendered as a native browser scrollbar rather than using media, thus providing the advantages of an independant scrollbar (support for rendering the scrollbar separate from the content it effects, support for "virtual scrolling" mechanisms where content size is unknown at initial render, etc), with a native look and feel and without requiring the loading of additional media on the page.

To enable this for a component simply set [Canvas.showCustomScrollbars](Canvas.md#attr-canvasshowcustomscrollbars) to true and set [Canvas.scrollbarConstructor](Canvas.md#attr-canvasscrollbarconstructor) to `"NativeScrollbar"`

---
## Method: NativeScrollbar.setScrollTarget

### Description
Sets or clears the scrollbar's scrollTarget. If no argument is provided, then the scrollTarget will be set to the scrollbar itself.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTarget | [Canvas](#type-canvas) | true | — | target canvas to be scrolled |

### Groups

- scroll

---
