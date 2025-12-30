# Hilite Documentation

[← Back to API Index](../reference.md)

---

## Attr: Hilite.fieldName

### Description
Name of the field, or array of fieldNames, this hilite should be applied to.

If unset, hilite is applied to every field of the record.

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.id

### Description
Unique id for this hilite definition.

For hilites that include [Hilite.criteria](#attr-hilitecriteria) this is not required.

If you are explicitly marking records for hiliting, set [DataBoundComponent.hiliteProperty](DataBoundComponent.md#attr-databoundcomponenthiliteproperty) on the record to this id.

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.icon

### Description
URL of an icon to show when this hilite is applied to a cell. Position of the icon is controlled by [DataBoundComponent.hiliteIconPosition](DataBoundComponent.md#attr-databoundcomponenthiliteiconposition) or [ListGridField.hiliteIconPosition](ListGridField.md#attr-listgridfieldhiliteiconposition).

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.htmlValue

### Description
Value to show **in place of** the actual value from the record, for a record that matches this hilite.

This can be used to take ranges of numeric values and simplify them to "Low", "Medium", "High" or similar textual values, translate very small or very large values to "Outlier" or "Negligible", and similar use cases.

### Groups

- hiliting

**Deprecated**

**Flags**: IR

---
## Attr: Hilite.replacementValue

### Description
HTML which replaces the cell's textual value where this hilite is applied.

Note that sorting, filtering, etc behavior will still operate on the underlying value. For example, if there is a date field with the FilterEditor enabled, the default search interface will still offer date-range based filtering even if hilites have caused values to be displayed as text such as "current" or "past due".

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.cssText

### Description
CSS text to be applied to cells where this hilite is applied, for example, "background-color:#FF0000"

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.htmlAfter

### Description
HTML to append to the end of cell values where this hilite is applied.

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.title

### Description
User-visible title for this hilite. Used for interfaces such as menus that can enable or disable hilites.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: Hilite.backgroundColor

### Description
When edited via a [HiliteEditor](HiliteEditor.md#class-hiliteeditor), the value for the background color of this hilite. If this is omitted, it will be automatically derived from the _backgroundColor_ attribute of [Hilite.cssText](#attr-hilitecsstext). When a hilite is saved in a HiliteEditor, both attributes are set automatically.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: Hilite.canEdit

### Description
Can highlight be edited from header context menu? Setting attribute to `false` prevents editing. A `null` or `true` value allows editing.

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.disabled

### Description
Whether this hilite is currently disabled.

Hilites can be programmatically enabled and disabled via [DataBoundComponent.enableHilite](DataBoundComponent.md#method-databoundcomponentenablehilite).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: Hilite.textColor

### Description
When edited via a [HiliteEditor](HiliteEditor.md#class-hiliteeditor), the value for the foreground color of this hilite. If this is omitted, it will be automatically derived from the _textColor_ attribute of [Hilite.cssText](#attr-hilitecsstext). When a hilite is saved in a HiliteEditor, both attributes are set automatically.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: Hilite.htmlBefore

### Description
HTML to pre-pend to cell values where this hilite is applied.

### Groups

- hiliting

**Flags**: IR

---
## Attr: Hilite.criteria

### Description
Criteria defining what records this hilite should apply to.

### Groups

- hiliting

**Flags**: IR

---
