# Deck Documentation

[← Back to API Index](../reference.md)

---

## Class: Deck

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A simple container that implements the policy that at most one of its contained components is visible at any given time.

The set of mutually exclusive components is specified by [Deck.panes](#attr-deckpanes), and whichever component is visible fills the space of the `Deck` automatically.

To switch to a new pane, call [Deck.setCurrentPane](#method-decksetcurrentpane), or simply call [show()](Canvas.md#method-canvasshow) on the pane directly - the `Deck` will notice that you have shown a different pane and hide other panes automatically.

[Deck.children](Canvas.md#attr-canvaschildren) may also be used; any components that are specified as children are unmanaged by the `Deck` and so can place themselves arbitrarily.

`Deck` achieves its mutually-exclusive display behavior by using the superclass [Layout.members](Layout.md#attr-layoutmembers) property, which means that properties such as [Layout.layoutMargin](Layout.md#attr-layoutlayoutmargin) and [Layout.vPolicy](Layout.md#attr-layoutvpolicy) do apply to deck. However, trying to manipulate `deck.members` with APIs such as [Layout.addMember](Layout.md#method-layoutaddmember) is not supported and will have undefined results.

---
## Attr: Deck.members

### Description
An array of canvases that will be contained within this layout. You can set the following properties on these canvases (in addition to the standard component properties):

*   [layoutAlign](Canvas.md#attr-canvaslayoutalign) -- specifies the member's alignment along the breadth axis; valid values are "top", "center" and "bottom" for a horizontal layout and "left", "center" and "right" for a vertical layout (see [Layout.defaultLayoutAlign](Layout.md#attr-layoutdefaultlayoutalign) for default implementation.)
*   [showResizeBar](Canvas.md#attr-canvasshowresizebar) -- set to true to show a resize bar (default is false)

Height and width settings found on members are interpreted by the Layout according to the [layout policy](Layout.md#attr-layoutvpolicy).

As an alternative to providing Canvas instances, the `members` array may also contain Strings. A String will be assumed to be a global ID, and a Canvas with that ID will be used as the member. Additionally, some Layout subclasses interpret certain special String values as references to automatically generated components (AutoChildren). See [ToolStrip.members](ToolStrip.md#attr-toolstripmembers) and [ListGrid.gridComponents](ListGrid_1.md#attr-listgridgridcomponents) for examples.

Note that it is valid to have null slots in the provided `members` Array, and the Layout will ignore those slots. This can be useful to keep code compact, for example, when constructing the `members` Array, you might use an expression that either returns a component or null depending on whether the component should be present. If the expression returns null, the null slot will be ignored by the Layout.

**Flags**: IR

---
## Attr: Deck.panes

### Description
Set of mutually exclusive panes displayed in this `Deck`.

If [Deck.currentPane](#attr-deckcurrentpane) is not set, when the `Deck` is first drawn, the first pane in this array becomes the `currentPane`.

**Flags**: IRW

---
## Attr: Deck.currentPane

### Description
The pane to show, including initially, in this `Deck`. All other panes are hidden.

The value identifies a widget in the [panes array](#attr-deckpanes) and can be directly set to a [widget](Canvas.md#class-canvas) or to the [local name](Canvas.md#attr-canvasname), [local ID](Canvas.md#method-canvasgetlocalid) or [global ID](Canvas.md#method-canvasgetid) of a widget.

**Flags**: IRW

---
## Method: Deck.removePane

### Description
Remove a pane from this deck.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas) | false | — | pane to remove |

---
## Method: Deck.hideCurrentPane

### Description
Hides the current pane, without showing any other pane.

---
## Method: Deck.setCurrentPane

### Description
Change the [CurrentPane](../reference.md#type-currentpane).

If the passed pane is not contained in this `Deck`, logs a warning and does nothing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas)|[GlobalId](../reference.md#type-globalid) | false | — | the pane to show, as either a `Canvas` or the [Canvas.ID](Canvas.md#attr-canvasid) |

---
## Method: Deck.addPane

### Description
Add a pane to this deck. If the specified pane is already present in the deck, it will be moved to the specified position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas) | false | — | pane to add |
| index | [Integer](../reference_2.md#type-integer) | true | — | position for the new pane in the [panes](#attr-deckpanes) array. If no index is specified, the pane will be added to the end of the panes array. |

---
## Method: Deck.currentPaneChanged

### Description
Notification fired when the `Deck`'s [currentPane](#attr-deckcurrentpane) is changed. This notification will occur even if the pane is changed prior to the deck being drawn or while the deck is hidden.

No notification is triggered, however, when the deck is drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| currentPane | [Canvas](#type-canvas) | false | — | the new `currentPane`, or null if no pane is currently visible. |

---
