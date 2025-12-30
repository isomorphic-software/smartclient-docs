# NavPanel Documentation

[← Back to API Index](../reference.md)

---

## Class: NavPanel

*Inherits from:* [SplitPane](SplitPane.md#class-splitpane)

### Description
Provides a list or tree of [navigation items](../reference.md#object-navitem), each of which specifies a component to be displayed in a mutually exclusive fashion in the [navDeck](#attr-navpanelnavdeck).

A NavPanel can either have a flat list of `NavItems` or a hierarchy via [NavItem.items](NavItem.md#attr-navitemitems) - use [NavPanel.isTree](#attr-navpanelistree) to explicitly control this.

Because NavPanel extends [SplitPane](SplitPane.md#class-splitpane), it automatically shifts between side-by-side vs single panel display on handset-sized devices. Specifically, the [NavPanel.navGrid](#attr-navpanelnavgrid) is set as the [SplitPane.navigationPane](SplitPane.md#attr-splitpanenavigationpane) and the [NavPanel.navDeck](#attr-navpanelnavdeck) is set as the [SplitPane.detailPane](SplitPane.md#attr-splitpanedetailpane).

Note that `NavPanel` is a fairly simple component to replicate by composing other SmartClient widgets. If you need a component that looks roughly like a `NavPanel` but will require lots of visual and behavioral customization, consider using the underlying components directly instead of deeply customizing the `NavPanel` class. A `NavPanel` is essentially just a [TreeGrid](TreeGrid.md#class-treegrid) and [Deck](Deck.md#class-deck) in a [SplitPane](SplitPane.md#class-splitpane), with a [recordClick](ListGrid_2.md#method-listgridrecordclick) handler to call [Deck.setCurrentPane](Deck.md#method-decksetcurrentpane) with a component ID stored as an attribute of each Record.

---
## Attr: NavPanel.headerStyle

### Description
CSS style used when [NavItem.isHeader](NavItem.md#attr-navitemisheader) is set on an item. May be overridden for a specific header item by [NavItem.customStyle](NavItem.md#attr-navitemcustomstyle).

**Flags**: IR

---
## Attr: NavPanel.navGrid

### Description
The [TreeGrid](TreeGrid.md#class-treegrid) used to display [NavItem](../reference.md#object-navitem)s.

**Flags**: IR

---
## Attr: NavPanel.isTree

### Description
Whether the [NavItem](../reference.md#object-navitem)s form a [Tree](Tree.md#class-tree) or are just a flat list. If `isTree` is false, [TreeGrid.showOpener](TreeGrid.md#attr-treegridshowopener) will be set false on the [NavPanel.navGrid](#attr-navpanelnavgrid) so that space isn't wasted.

The setting for `isTree` is defaulted immediately before initial draw, based on whether any [NavItem](../reference.md#object-navitem) has a list of subitems specified via [NavItem.items](NavItem.md#attr-navitemitems). If no [NavItem](../reference.md#object-navitem)s are provided before draw, `isTree` defaults to `true`. Auto-detection is never attempted again even if all `NavItems` are replaced.

Set `isTree` explicitly if auto-detection doesn't yield the correct result for your application.

**Flags**: IR

---
## Attr: NavPanel.currentItem

### Description
The current [NavItem](../reference.md#object-navitem) whose [pane](NavItem.md#attr-navitempane) is showing in the [navDeck](#attr-navpanelnavdeck). This must be an item of this `NavPanel` if set.

**Flags**: IRW

---
## Attr: NavPanel.navDeck

### Description
The [Deck](Deck.md#class-deck) area where components specified via [NavItem.pane](NavItem.md#attr-navitempane) are displayed.

**Flags**: IR

---
## Attr: NavPanel.currentItemId

### Description
The ID of the current [NavItem](../reference.md#object-navitem) whose [pane](NavItem.md#attr-navitempane) is showing in the [navDeck](#attr-navpanelnavdeck). The `NavItem` must be an item of this `NavPanel` if set.

The ID of a `NavItem` is the item's [NavItem.id](NavItem.md#attr-navitemid) if set; otherwise, it is the ID of the item's [NavItem.pane](NavItem.md#attr-navitempane), though `currentItemId` may be initialized to either identifier.

**Flags**: IRW

---
## Attr: NavPanel.defaultToFirstItem

### Description
Select the first [NavItem](../reference.md#object-navitem) on initialization if neither [NavPanel.currentItemId](#attr-navpanelcurrentitemid) nor [NavPanel.currentItem](#attr-navpanelcurrentitem) are provided.

**Flags**: IRW

---
## Attr: NavPanel.navItems

### Description
Top-level navigation items to display. You can optionally specify a tree of items using [NavItem.items](NavItem.md#attr-navitemitems).

A separator between navigation items can be created by setting [NavItem.isSeparator](NavItem.md#attr-navitemisseparator), and a header can be created via [NavItem.isHeader](NavItem.md#attr-navitemisheader).

Each non-separator and non-header `NavItem` specifies a component to be displayed in the [NavPanel.navDeck](#attr-navpanelnavdeck) via [NavItem.pane](NavItem.md#attr-navitempane).

`NavItem`s can also be individually styled via [ListGridRecord._baseStyle](ListGridRecord.md#attr-listgridrecord_basestyle) or [NavItem.customStyle](NavItem.md#attr-navitemcustomstyle).

**Flags**: IRW

---
## Method: NavPanel.setCurrentItem

### Description
Setter for [NavPanel.currentItem](#attr-navpanelcurrentitem). Note that [NavPanel.currentItemId](#attr-navpanelcurrentitemid) is also updated by this setter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCurrentItem | [NavItem](#type-navitem) | true | — | the new `currentItem`. May be `null` to hide the current item. If `newCurrentItem` is a separator or header item, then setCurrentItem() has no effect. |

---
## Method: NavPanel.setCurrentItemId

### Description
Setter for [NavPanel.currentItemId](#attr-navpanelcurrentitemid). Note that [NavPanel.currentItem](#attr-navpanelcurrentitem) is also updated by this setter and `this.currentItemId` may be normalized to a different identifier.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCurrentItemId | [Identifier](../reference.md#type-identifier) | true | — | the ID of the new current item, which may be either the item's [NavItem.id](NavItem.md#attr-navitemid) or the ID of the item's [NavItem.pane](NavItem.md#attr-navitempane). May be `null` or an empty string to hide the current item. If the item with ID `newCurrentItemId` is a separator or header item, then setCurrentItemId() has no effect. |

---
