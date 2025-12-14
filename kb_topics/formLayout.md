# Form Layout

[← Back to API Index](../reference.md)

---

## KB Topic: Form Layout

### Description
**FormItem Placement in Columns and Rows**

With the default tabular layout mechanism, items are laid out in rows from left to right until the number of columns, specified by [form.numCols](../classes/DynamicForm.md#attr-dynamicformnumcols), is filled, then a new row is begun. Flags on FormItems, including [startRow](../classes/FormItem.md#attr-formitemstartrow), [endRow](../classes/FormItem.md#attr-formitemendrow), [colSpan](../classes/FormItem.md#attr-formitemcolspan) and [rowSpan](../classes/FormItem.md#attr-formitemrowspan), control row and column placement and spanning.

Note that the most common form items (TextItem, SelectItem, etc) take up **two** columns by default: one for the form control itself, and one for it's title. The default setting of [form.numCols:2](../classes/DynamicForm.md#attr-dynamicformnumcols) will result in one TextItem or SelectItem per row.

Note also that ButtonItems have both startRow:true and endRow:true by default. You must set startRow and/or endRow to `false` on a ButtonItem in order to place a button in the same row as any other item.

The log category "tablePlacement" can be enabled from the Developer Console to watch items being placed. You can also set [form.cellBorder:1](../classes/DynamicForm.md#attr-dynamicformcellborder) to reveal the table structure for layout troubleshooting purposes.

**Row and Column Sizing**

[DynamicForm.colWidths](../classes/DynamicForm.md#attr-dynamicformcolwidths) controls the widths of form columns. FormItems that have "\*" for [FormItem.width](../classes/FormItem.md#attr-formitemwidth) will fill the column. FormItems with a numeric width will have that width in pixels regardless of the column's specified width, which may cause the column to overflow as described under [DynamicForm.fixedColWidths](../classes/DynamicForm.md#attr-dynamicformfixedcolwidths).

For row heights, the largest pixel height specified on any item in the row is taken as a minimum size for the row. Then, any rows that have "\*" or "%" height items will share any height not taken up by fixed-sized items.

Individual item heights are controlled by [item.height](../classes/FormItem.md#attr-formitemheight). This may be specified as an integer (pixel value), or a percentage string, or the special string "\*", which indicates an item should fill the available space.  
Percentages allow developers to determine how the available space in the form is split amongst items. For example if a form has 4 items in a single column, 2 of which have an absolute pixel height specified, and 2 of which are have heights of `"30%"` and `"70%"` respectively, the percentage sized items will split up the available space after the fixed size items have been rendered.  
Note that [item.cellHeight](../classes/FormItem.md#attr-formitemcellheight) may be specified to explicitly control the height of an item's cell. In this case the specified [item.height](../classes/FormItem.md#attr-formitemheight) will govern the size of the item within the cell (and if set to a percentage, this will be interpreted as a percentage of the cellHeight).

**Managing Overflow**

Forms often contain labels, data values, or instructional text which can vary in size based on the skin, data values, or internationalization settings. There are a few ways to deal with a form potentially varying in size:

1.  Allow scrolling when necessary, using [overflow:auto](../classes/Canvas.md#attr-canvasoverflow), either on the immediate form, or on some parent.
2.  Place the form in a Layout along with a component that can render any specified size, such as a [ListGrid](../classes/ListGrid_1.md#class-listgrid). In this case, the Layout will automatically shrink the grid in order to accommodate the form.
3.  Ensure that the form can always render at a designed minimum size by reducing the number of cases of variable-sized text, and testing remaining cases across all supported skins. For example, move help text into hovers on help icons, or clip long text values at a maximum length and provide a hover to see the rest.

**Adaptive Layout**

To have various automatic adjustments made to render your form items in a single column, you can use [linearMode](../classes/DynamicForm.md#attr-dynamicformlinearmode). Importantly, you can have this mode automatically applied to a form on [handset devices](../classes/Browser.md#classattr-browserishandset) by setting [linearOnMobile](../classes/DynamicForm.md#attr-dynamicformlinearonmobile) true. For further details and the properties that are available to customize this mode, see the [linearMode](../classes/DynamicForm.md#attr-dynamicformlinearmode) documentation.

Several examples of Form Layout are available *here*.

### Related

- [DynamicForm.itemLayout](../classes/DynamicForm.md#attr-dynamicformitemlayout)
- [DynamicForm.linearMode](../classes/DynamicForm.md#attr-dynamicformlinearmode)
- [DynamicForm.linearOnMobile](../classes/DynamicForm.md#attr-dynamicformlinearonmobile)
- [DynamicForm.numCols](../classes/DynamicForm.md#attr-dynamicformnumcols)
- [DynamicForm.linearNumCols](../classes/DynamicForm.md#attr-dynamicformlinearnumcols)
- [DynamicForm.fixedColWidths](../classes/DynamicForm.md#attr-dynamicformfixedcolwidths)
- [DynamicForm.colWidths](../classes/DynamicForm.md#attr-dynamicformcolwidths)
- [DynamicForm.minColWidth](../classes/DynamicForm.md#attr-dynamicformmincolwidth)
- [DynamicForm.cellPadding](../classes/DynamicForm.md#attr-dynamicformcellpadding)
- [DynamicForm.cellBorder](../classes/DynamicForm.md#attr-dynamicformcellborder)
- [DynamicForm.sectionVisibilityMode](../classes/DynamicForm.md#attr-dynamicformsectionvisibilitymode)
- [FormItem.width](../classes/FormItem.md#attr-formitemwidth)
- [FormItem.linearWidth](../classes/FormItem.md#attr-formitemlinearwidth)
- [FormItem.height](../classes/FormItem.md#attr-formitemheight)
- [FormItem.staticHeight](../classes/FormItem.md#attr-formitemstaticheight)
- [FormItem.titleColSpan](../classes/FormItem.md#attr-formitemtitlecolspan)
- [FormItem.colSpan](../classes/FormItem.md#attr-formitemcolspan)
- [FormItem.linearColSpan](../classes/FormItem.md#attr-formitemlinearcolspan)
- [FormItem.rowSpan](../classes/FormItem.md#attr-formitemrowspan)
- [FormItem.startRow](../classes/FormItem.md#attr-formitemstartrow)
- [FormItem.endRow](../classes/FormItem.md#attr-formitemendrow)
- [FormItem.linearStartRow](../classes/FormItem.md#attr-formitemlinearstartrow)
- [FormItem.linearEndRow](../classes/FormItem.md#attr-formitemlinearendrow)
- [ButtonItem.startRow](../classes/ButtonItem.md#attr-buttonitemstartrow)
- [ButtonItem.endRow](../classes/ButtonItem.md#attr-buttonitemendrow)
- [SelectItem.height](../classes/SelectItem.md#attr-selectitemheight)
- [TextAreaItem.staticHeight](../classes/TextAreaItem.md#attr-textareaitemstaticheight)

### See Also

- [FormItem.width](../classes/FormItem.md#attr-formitemwidth)
- [FormItem.height](../classes/FormItem.md#attr-formitemheight)
- [DynamicForm.itemLayout](../classes/DynamicForm.md#attr-dynamicformitemlayout)

---
