# NavItem Documentation

[← Back to API Index](../reference.md)

---

## Attr: NavItem.pane

### Description
Component to display in the [NavPanel.navDeck](NavPanel.md#attr-navpanelnavdeck) when this `NavItem` is selected.

A component can be provided directly, or its ID can be provided.

**Flags**: IR

---
## Attr: NavItem.isHeader

### Description
If set, this `NavItem` will be styled like a header. In this case [NavItem.pane](#attr-navitempane) is ignored and nothing happens when the header is clicked. However, [NavItem.items](#attr-navitemitems) can still be configured to place items hierarchically under the header.

**Flags**: IR

---
## Attr: NavItem.icon

### Description
Icon to show for this `NavItem`. If not specified, the ${isc.DocUtils.linkForRef('attr:TreeGrid.folderIcon','navGrid\\'s folderIcon')} is used.

**Flags**: IR

---
## Attr: NavItem.isSeparator

### Description
If set, this `NavItem` will be styled as a separator. A separator does not have a [pane](#attr-navitempane) and nothing happens when the separator is clicked.

**Flags**: IR

---
## Attr: NavItem.title

### Description
Title to show for this `NavItem`.

**Flags**: IR

---
## Attr: NavItem.id

### Description
An optional ID for this `NavItem`. If specified, this must be unique within the `NavPanel`.

**Flags**: IR

---
## Attr: NavItem.customStyle

### Description
CSS style name used for this `NavItem`. If set and this `NavItem` is a [header](#attr-navitemisheader), this overrides the `NavPanel`'s [NavPanel.headerStyle](NavPanel.md#attr-navpanelheaderstyle).

**Flags**: IR

---
## Attr: NavItem.items

### Description
Optional subitems of this `NavItem`.

**Flags**: IR

---
