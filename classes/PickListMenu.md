# PickListMenu Documentation

[← Back to API Index](../reference.md)

---

## Class: PickListMenu

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
[ListGrid](ListGrid_1.md#class-listgrid) subclass used, by default, by FormItems which implement [PickList](../reference_2.md#interface-picklist) to display a [flat list](PickList.md#attr-picklistdatasettype) of selectable options.

Can be subclassed, customized and assigned to FormItems via the [pickListConstructor](ComboBoxItem.md#attr-comboboxitempicklistconstructor) attribute.

---
## Attr: PickListMenu.canSaveSearches

### Description
Option to save searches is disabled for PickListMenus

**Flags**: IRA

---
## Attr: PickListMenu.canShowFilterEditor

### Description
Option to show filter editor is disabled for pickListMenus by default

**Flags**: IRA

---
## Attr: PickListMenu.normalCellHeight

### Description
If [ListGrid.baseStyle](ListGrid_1.md#attr-listgridbasestyle) is unset, base style will be derived from [ListGrid.normalBaseStyle](ListGrid_1.md#attr-listgridnormalbasestyle) if this grid has fixed row heights and the specified [ListGrid.cellHeight](ListGrid_1.md#attr-listgridcellheight) matches this value. Otherwise [ListGrid.tallBaseStyle](ListGrid_1.md#attr-listgridtallbasestyle) will be used.

**Flags**: IRWA

---
## Attr: PickListMenu.dataProperties

### Description
For databound ListGrids, this attribute can be used to customize the [ResultSet](ResultSet.md#class-resultset) object created for this grid when data is fetched

### Groups

- databinding

**Flags**: IRWA

---
## Attr: PickListMenu.bodyStyleName

### Description
CSS style used for the body of this grid. If applying a background-color to the body via a CSS style applied using this property, be sure to set [ListGrid.bodyBackgroundColor](ListGrid_1.md#attr-listgridbodybackgroundcolor) to `null`.

### Groups

- appearance

**Flags**: IRW

---
## Attr: PickListMenu.styleName

### Description
Default CSS class for the ListGrid as a whole.

### Groups

- appearance

**Flags**: IRW

---
## Attr: PickListMenu.emptyMessage

### Description
The string to display in the body of a listGrid with an empty data array, if showEmptyMessage is true.

### Groups

- i18nMessages

### See Also

- [GridRenderer.showEmptyMessage](GridRenderer.md#attr-gridrenderershowemptymessage)
- [GridRenderer.emptyMessageStyle](GridRenderer.md#attr-gridrendereremptymessagestyle)

**Flags**: IRW

---
## Method: PickListMenu.applySelection

### Description
When this PickListMenu is associated with a [FormItem](FormItem.md#class-formitem), this method applies the current selection from this PickList to the associated FormItem.

---
