# Skin Variants

[← Back to API Index](../reference.md)

---

## KB Topic: Skin Variants

### Description
Skin variants are named visual presets that modify a base class's appearance without changing behavior. Each variant is a set of property overrides registered in [Variant](../classes/Variant.md#class-variant) and auto-created as a subclass during framework initialization.

Variant subclasses work in any skin. When a skin provides CSS definitions for the variant's style properties, the variant takes effect. In skins that do not define those CSS classes, variant style properties automatically revert to their superclass values via [Canvas.autoRevertStyles](../classes/Canvas.md#attr-canvasautorevertstyles), so the component falls back to the skin's default appearance.

#### Grid variants
Grid variants (Compact, Flat, Bordered, Striped) are created as subclasses of both [ListGrid](../classes/ListGrid_1.md#class-listgrid) and [TreeGrid](../classes/TreeGrid.md#class-treegrid). For example, the Compact variant produces both `CompactGrid` and `CompactTreeGrid`.

The "Default Table" appearance in variant-enabled skins is simply a standard [ListGrid](../classes/ListGrid_1.md#class-listgrid) with features enabled (filtering, grouping, inline editing, row selection) — it is not a variant. Similarly, [TreeGrid](../classes/TreeGrid.md#class-treegrid) renders with the default tree appearance.

#### Usage
```
 // Use the auto-created subclass
 isc.PillButton.create({ title: "Pill Button" });
 isc.CompactGrid.create({ fields: [...], dataSource: "myDS" });

 // Or apply variant properties to a plain instance
 var props = isc.Variant.getVariant("PillButton").properties;
 isc.Button.create(isc.addProperties({ title: "Hi" }, props));
 
```

### Related

- [PillButton](../reference.md#class-pillbutton)
- [GhostButton](../reference.md#class-ghostbutton)
- [OutlineButton](../reference.md#class-outlinebutton)
- [SoftButton](../reference.md#class-softbutton)
- [LinkButton](../reference.md#class-linkbutton)
- [DangerButton](../reference.md#class-dangerbutton)
- [SuccessButton](../reference.md#class-successbutton)
- [CircleButton](../reference.md#class-circlebutton)
- [WhiteButton](../reference.md#class-whitebutton)
- [UnderlineTabSet](../reference.md#class-underlinetabset)
- [PillTabSet](../reference.md#class-pilltabset)
- [CardTabSet](../reference.md#class-cardtabset)
- [MinimalTextItem](../reference.md#class-minimaltextitem)
- [RoundedTextItem](../reference.md#class-roundedtextitem)
- [FilledTextItem](../reference.md#class-filledtextitem)
- [Card](../classes/Card.md#class-card)
- [ElevatedCard](../reference.md#class-elevatedcard)
- [FlatCard](../reference.md#class-flatcard)
- [BorderedCard](../reference.md#class-borderedcard)
- [CardPanel](../reference.md#class-cardpanel)
- [ElevatedPanel](../reference.md#class-elevatedpanel)
- [FlatPanel](../reference.md#class-flatpanel)
- [BorderedPanel](../reference.md#class-borderedpanel)
- [DarkWindow](../reference.md#class-darkwindow)
- [TranslucentWindow](../reference.md#class-translucentwindow)
- [FlatGrid](../reference.md#class-flatgrid)
- [FlatTreeGrid](../reference.md#class-flattreegrid)
- [StripedGrid](../reference.md#class-stripedgrid)
- [StripedTreeGrid](../reference.md#class-stripedtreegrid)
- [CompactGrid](../reference.md#class-compactgrid)
- [CompactTreeGrid](../reference.md#class-compacttreegrid)
- [BorderedGrid](../reference.md#class-borderedgrid)
- [BorderedTreeGrid](../reference.md#class-borderedtreegrid)
- [RoundedMenu](../reference.md#class-roundedmenu)
- [CompactMenu](../reference.md#class-compactmenu)
- [BorderedSection](../reference.md#class-borderedsection)
- [GradientHeader](../reference.md#class-gradientheader)
- [MinimalSection](../reference.md#class-minimalsection)
- [Canvas.autoRevertStyles](../classes/Canvas.md#attr-canvasautorevertstyles)

---
