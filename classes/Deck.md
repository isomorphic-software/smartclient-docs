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
## Attr: Deck.panes

### Description
Set of mutually exclusive panes displayed in this `Deck`.

If [Deck.currentPane](#attr-deckcurrentpane) is not set, when the `Deck` is first drawn, the first pane in this array becomes the `currentPane`.

**Flags**: IRW

---
## Attr: Deck.currentPane

### Description
The pane currently shown in this `Deck`. All other panes are hidden.

**Flags**: IRW

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
