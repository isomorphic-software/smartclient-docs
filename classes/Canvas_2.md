# Canvas Documentation (Part 2 of 2)

[← Back to API Index](../reference.md)

---

## Method: Canvas.visibleAtPoint

### Description
Does this widget contain the specified global (x,y) coordinates, and have no other widgets also at the specified position, obscuring this one? This is commonly used for (for example) drag and drop interactions.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [number](#type-number) | false | — | GLOBAL x-coordinate |
| y | [number](#type-number) | false | — | GLOBAL y-coordinate |
| withinViewport | [boolean](../reference.md#type-boolean) | true | — | point lies within our viewport rather than just our drawn area |
| ignoreWidgets | [Canvas](#type-canvas) | true | — | If passed ignore widget(s), do not check whether those widgets occludes this one. |
| upToParent | [Canvas](#type-canvas) | true | — | If passed, only check for siblings occluding the component up as far as the specified parent widget. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this object contains the specified point; false otherwise

### Groups

- positioning

**Flags**: A

---
## Method: Canvas.removeChild

### Description
Remove a child from this parent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [Canvas](#type-canvas) | false | — | Child canvas to remove from this parent. |
| name | [String](#type-string) | true | — | If the child canvas was assigned a name when added via addChild(), it should be passed in here to ensure no reference is kept to the child |

### Groups

- containment

---
## Method: Canvas.getAriaHandleID

### Description
Returns the DOM ID for the main element for this canvas which will have ARIA [role](Canvas_1.md#attr-canvasariarole) and [attributes](Canvas_1.md#attr-canvasariastate) applied to it. This can be useful when applying [custom aria state attributes](Canvas_1.md#attr-canvasariastate) which need to refer to the DOM handle of another canvas, such as [aria-controls](https://www.w3.org/TR/2017/REC-wai-aria-1.1-20171214/#aria-controls).

Note that we do not recommend using this ID to identify the element in the DOM for integration with automated testing tools. The [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) and [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) APIs should be used instead. These locators are much finer grained - they allow developers to identify sub-elements within the widget handle that map to specific logical SmartClient objects (for example FormItem Icons within a DynamicForm). They are also more stable - AutoTest locators are able to reliably identify components based on their position in the application hierarchy and other context, while the DOM element IDs are not guaranteed not to change across page reloads.

### Returns

`[String](#type-string)` — ID written into the DOM element for this component

**Flags**: A

---
## Method: Canvas.deparent

### Description
Remove this canvas from its parent if it has one.

### Groups

- containment

---
## Method: Canvas.setSnapTo

### Description
Set the snapTo property of this canvas, and handle repositioning.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| snapTo | [String](#type-string) | false | — | new snapTo value |

### Groups

- snapGridDragging

---
## Method: Canvas.setLeft

### Description
Set the left coordinate of this object, relative to its enclosing context, in pixels. NOTE: if you're setting multiple coordinates, use setRect(), moveTo() or resizeTo() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Number](#type-number)|[String](#type-string) | false | — | new left coordinate |

### Groups

- positioning

---
## Method: Canvas.setOverflow

### Description
Update the [overflow](Canvas_1.md#attr-canvasoverflow) of a Canvas after it has been created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newOverflow | [Overflow](../reference.md#type-overflow) | false | — | New overflow value. |

### Groups

- positioning
- sizing
- sizing

**Flags**: A

---
## Method: Canvas.setPadding

### Description
Set the CSS padding of this component, in pixels. Padding provides space between the border and the component's contents.

This property sets the same thickness of padding on every side. Differing per-side padding can be set in a CSS style and applied via [Canvas.styleName](Canvas_1.md#attr-canvasstylename).

While grouped, updates [Canvas.groupPadding](Canvas_1.md#attr-canvasgrouppadding) and applies it immediately, preserving the saved ungrouped padding described by [Canvas.padding](Canvas_1.md#attr-canvaspadding). Passing null clears the explicit padding, allowing [Canvas.styleName](Canvas_1.md#attr-canvasstylename) to apply.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPadding | [number](#type-number) | false | — | new padding in pixels |

### Groups

- appearance

---
## Method: Canvas.doValueDictation

### Description
If [Canvas.supportsVoiceCommands](Canvas_1.md#method-canvassupportsvoicecommands) returns true, this method may be implemented to deal with transcriptions recorded while this Canvas has focus.

If focus is in this canvas when the user double-taps the [voice-key](VoiceAssist.md#classattr-voiceassistvoicekey), records some speech and double-taps again, this method is invoked with the final dictated-text, allowing the canvas to display it or process it in some way, such as saving it to a database or providing it to an AI for processing.

Note that, if the canvas has a `setValue` method, the transcription will be applied automatically and interactively as the user speaks. If that functionality suits your needs, there is no need to implement this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| text | [String](#type-string) | false | — | the final text as spoken by the user |

---
## Method: Canvas.getScrollBottom

### Description
Returns the scrollTop required to scroll vertically to the end of this widget's content.

### Returns

`[int](../reference.md#type-int)` — scroll bottom coordinate

### Groups

- scrolling

---
## Method: Canvas.scrollToTop

### Description
Vertically scrolls the content of the widget to 0

### Groups

- scrolling

---
## Method: Canvas.setMinHeight

### Description
Resizes the widget vertically if required to satisfy the specified [Canvas.minHeight](Canvas_1.md#attr-canvasminheight).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [number](#type-number) | false | — | new minimum height |

### Groups

- sizing

---
## Method: Canvas.getRect

### Description
Returns the coordinates of this object as an array in left, top, width, height order.

### Returns

`[Array of int](#type-array-of-int)` — coordinates as \[left, top, width, height\]

### Groups

- positioning
- sizing

---
