# PortalLayout Documentation

[← Back to API Index](../main.md)

---

## Class: PortalLayout

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A PortalLayout is a special subclass of Layout designed to display [Portlet](Portlet.md#class-portlet) windows. A PortalLayout displays Portlets in columns and supports drag-drop interaction for moving Portlets around within the PortalLayout. Portlets may be drag-reordered within columns, dragged into other columns, or dragged next to other Portlets to sit next to them horizontally within a column. See [portalLayoutDrop](../kb_topics/portalLayoutDrop.md#kb-topic-drag-and-drop-behavior-within-portallayouts) for a discussion of drag and drop behavior within PortalLayouts.

---
## Attr: PortalLayout.numColumns

### Description
Initial number of columns to show in this PortalLayout. Note that after initialization columns should be added / removed via [PortalLayout.addColumn](#method-portallayoutaddcolumn) and [PortalLayout.removeColumn](#method-portallayoutremovecolumn). numColumns is ignored if you initialize the [PortalLayout.portlets](#attr-portallayoutportlets) attribute, since the portlets attribute will imply how many columns to create.

### See Also

- [PortalLayout.portlets](#attr-portallayoutportlets)

**Flags**: IR

---
## Attr: PortalLayout.canAddColumns

### Description
Can the user add columns to this PortalLayout?

Columns may be added via the [column menu](#attr-portallayoutshowcolumnmenus), or by dragging a portlet and dropping next to an existing column, if [PortalLayout.dropTypes](#attr-portallayoutdroptypes) includes the drop type for the portlet.

Note that if [PortalLayout.removeEmptyColumns](#attr-portallayoutremoveemptycolumns) is true, when the user drags every portlet out of a portalLayout column, the column will be removed automatically.

**Flags**: IRW

---
## Attr: PortalLayout.overflow

### Description
Controls how the PortalLayout reacts when column widths or [Portlet](Portlet.md#class-portlet) widths overflow the width of the PortalLayout. By default, the PortalLayout scrolls when necessary. You can also use overflow: visible or overflow: hidden, with the usual results -- see [PortalLayout.canResizePortlets](#attr-portallayoutcanresizeportlets) for a further explanation of column widths.

Note that overflowing height is also affected by [columnOverflow](#attr-portallayoutcolumnoverflow). By default, each column will scroll individually -- you can change columnOverflow to "auto" to scroll the whole PortalLayout instead.

### Groups

- sizing

### See Also

- [PortalLayout.canResizePortlets](#attr-portallayoutcanresizeportlets)
- [PortalLayout.columnOverflow](#attr-portallayoutcolumnoverflow)
- [Canvas.overflow](Canvas.md#attr-canvasoverflow)

**Flags**: IRW

---
## Attr: PortalLayout.canResizePortlets

### Description
Should the height and width of [Portlets](Portlet.md#class-portlet) be drag-resizable?

Note that changing the **height** of a Portlet will change the height of all the Portlets in the same row to match.

If the height of Portlets causes a column to overflow, that column will scroll vertically (independent of other columns), depending on the [columnOverflow](#attr-portallayoutcolumnoverflow) setting.

Changing the **width** of a Portlet will potentially cause columns to stretch and shrink their displayed widths in order to accommodate the Portlets, depending on the value of [canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths) and [canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths).

However, the instrinsic width of the columns will remain the same, so that the columns will resume their former widths when no longer necessary to stretch or shrink to accommodate the widths of Portlets. To allow drag-resizing of the intrinsic width of columns, see [canResizeColumns](#attr-portallayoutcanresizecolumns).

The net effect is that (by default) PortalLayouts behave like layouts when Portlet sizes do not cause overflow, but behave more like stacks when overflow occurs.

### Groups

- sizing

### See Also

- [PortalLayout.canResizeColumns](#attr-portallayoutcanresizecolumns)
- [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths)
- [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths)
- [PortalLayout.columnOverflow](#attr-portallayoutcolumnoverflow)

**Flags**: IRW

---
## Attr: PortalLayout.columnBorder

### Description
Border to show around columns in this PortalLayout

**Flags**: IRW

---
## Attr: PortalLayout.preventRowUnderflow

### Description
Controls whether the last [Portlet](Portlet.md#class-portlet) in a row will be stretched to fill the row's width, or left at its specified width.

### Groups

- sizing

**Flags**: IRW

---
## Attr: PortalLayout.portlets

### Description
A convenience attribute which you can use to populate a PortalLayout with [Portlets](Portlet.md#class-portlet) on initialization. After initialization, use [addPortlet()](#method-portallayoutaddportlet) or drag-and-drop to add Portlets, and [getPortlets()](#method-portallayoutgetportlets) or [getPortletArray()](#method-portallayoutgetportletarray) to get Portlets.

To create one column, you can provide an array of Portlets.

To create multiple columns, provide an array of arrays (where the first level represents columns, and the second represents Portlets).

To put multiple portlets in the same row, provide a third level to the array.

Note that [numColumns](#attr-portallayoutnumcolumns) is ignored if you provide the portlets attribute, since the array will indicate how many columns to create. You can provide an empty second-level array to create a blank column, if needed.

### See Also

- [PortalLayout.getPortlets](#method-portallayoutgetportlets)
- [PortalLayout.getPortletArray](#method-portallayoutgetportletarray)
- [PortalLayout.addPortlet](#method-portallayoutaddportlet)
- [PortalLayout.numColumns](#attr-portallayoutnumcolumns)

**Flags**: I

---
## Attr: PortalLayout.canShrinkColumnWidths

### Description
Controls whether the PortalLayout will shrink column widths to avoid overflowing the PortalLayout horizontally. If the PortalLayout would otherwise overflow its width, it will check each column to see whether it is wider than necessary to accommodate its [Portlets](Portlet.md#class-portlet). If so, the column may shrink to avoid having to scroll the PortalLayout.

### Groups

- sizing

### See Also

- [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths)

**Flags**: IRWA

---
## Attr: PortalLayout.canResizeColumns

### Description
Are columns in this PortalLayout drag-resizeable?

Note that the displayed width of a column will automatically shrink and stretch to accommodate the width of [Portlets](Portlet.md#class-portlet) -- see [canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths) and [canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths) for an explanation. This setting affects the intrinsic width of a column -- that is, the width it will try to return to when not necessary to stretch or shrink to accommodate Portlet widths.

### Groups

- sizing

### See Also

- [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths)
- [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths)

**Flags**: IRW

---
## Attr: PortalLayout.portletDropTypes

### Description
The [dropTypes](Canvas.md#attr-canvasdroptypes) to be applied when dropping [Portlets](Portlet.md#class-portlet) on this `PortalLayout`, or when dropping other components to be auto-wrapped in a [Portlet](Portlet.md#class-portlet). If you set this, then you will need to set an equivalent [Canvas.dragType](Canvas.md#attr-canvasdragtype) on anything to be dragged into this `PortalLayout` (including [Portlets](Portlet.md#class-portlet)).

As a convenience, [Portlet.dragType](Portlet.md#attr-portletdragtype) defaults to `"Portlet"`. Thus, if you want to allow [Portlets](Portlet.md#class-portlet) to be dropped on this `PortalLayout`, but disable auto-wrapping of other components, you can set `portletDropTypes` to `["Portlet"]`.

If you want to allow some [Portlets](Portlet.md#class-portlet) to be dropped on this `PortalLayout` but not others, then set a custom [dragType](Portlet.md#attr-portletdragtype) for the [Portlets](Portlet.md#class-portlet), and set `portletDropTypes` to match.

If you want to have different `dropTypes` for [rows](#attr-portallayoutrow) and [rowLayouts](#attr-portallayoutrowlayout), you can specify `dropType` on the [row](#attr-portallayoutrow) or [rowLayout](#attr-portallayoutrowlayout) autochildren instead.

For more control over what can be dropped, you can also implement [willAcceptPortletDrop()](#method-portallayoutwillacceptportletdrop).

### Groups

- dragdrop

### See Also

- [Canvas.dropTypes](Canvas.md#attr-canvasdroptypes)

**Flags**: IRW

---
## Attr: PortalLayout.row

### Description
Automatically generated horizontal [Layout](Layout.md#class-layout) used to create rows of [Portlets](Portlet.md#class-portlet) via [createAutoChild()](Class.md#method-classcreateautochild). Since this is an [AutoChild](../main.md#type-autochild), you can use rowDefaults and rowProperties to customize the rows.

Rows are created inside [rowLayouts](#attr-portallayoutrowlayout), which in turn are inside [columns](#attr-portallayoutcolumn).

### See Also

- [PortalLayout.column](#attr-portallayoutcolumn)
- [PortalLayout.rowLayout](#attr-portallayoutrowlayout)

**Flags**: A

---
## Attr: PortalLayout.portletHSpacing

### Description
The horizontal space between portlets placed into the same row.

To set the spacing between portal columns, use [PortalLayout.columnSpacing](#attr-portallayoutcolumnspacing).

### Groups

- sizing

### See Also

- [PortalLayout.portletVSpacing](#attr-portallayoutportletvspacing)
- [PortalLayout.columnSpacing](#attr-portallayoutcolumnspacing)

**Flags**: IRW

---
## Attr: PortalLayout.columnOverflow

### Description
Controls the [overflow](Canvas.md#attr-canvasoverflow) setting for each column. If set to "auto" (the default) then each column will scroll individually (if its [Portlets](Portlet.md#class-portlet) overflow the column height). You can also use "hidden" to clip overflowing heights, or "visible" to show the overflow. The effect of "visible" will depend on the setting for [PortalLayout.overflow](#attr-portallayoutoverflow) -- by default, the PortalLayout as a whole will scroll when necessary.

### Groups

- sizing

### See Also

- [Overflow](../main.md#type-overflow)
- [Canvas.overflow](Canvas.md#attr-canvasoverflow)

**Flags**: IRWA

---
## Attr: PortalLayout.preventUnderflow

### Description
Controls whether the last column will be stretched to fill the PortalLayout's width, or left at its specified width.

### Groups

- sizing

**Flags**: IRW

---
## Attr: PortalLayout.portletVSpacing

### Description
The vertical space between portal rows.

### Groups

- sizing

### See Also

- [PortalLayout.portletHSpacing](#attr-portallayoutportlethspacing)

**Flags**: IRW

---
## Attr: PortalLayout.stretchColumnWidthsProportionally

### Description
When [stretching column widths](#attr-portallayoutcanstretchcolumnwidths), should we stretch all column widths proportionally, or just stretch the columns that need extra width?

Note that this implies turning off [canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths).

### Groups

- sizing

### See Also

- [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths)
- [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths)

**Flags**: IRWA

---
## Attr: PortalLayout.showColumnMenus

### Description
Should a menu be shown within each column with options to add / remove columns?

**Flags**: IRW

---
## Attr: PortalLayout.canResizeRows

### Description
Should vertical drag-resize of portlets within columns be allowed?

**Deprecated**

**Flags**: IRW

---
## Attr: PortalLayout.preventColumnUnderflow

### Description
Controls whether the last [Portlet](Portlet.md#class-portlet) in a column will be stretched to fill the column's height, or left at its specified height.

### Groups

- sizing

**Flags**: IRW

---
## Attr: PortalLayout.portletHDropOffset

### Description
This property is used to determine the appropriate drop target for a component being dropped within this PortalLayout.

If [PortalLayout.canAddColumns](#attr-portallayoutcanaddcolumns) is true and the user hovers within `portletHDropOffset` pixels of the left or right edge of a column, the drop will be interpreted as a request to add a new column adjacent to that column.

If the user instead hovers within `portletHDropOffset` pixels of the left or right edge of a Portlet within an existing row, the drop will be interpreted as an attempt to insert the new Portlet into that row, next to the targeted Portlet.

When a Portlet is at the edge of a column (i.e., the first or last Portlet in a row), these horizontal drop zones overlap. In this case, the column-level drop zone is evaluated first: if the pointer is within the outermost offset, the drop will add a new column. If the pointer is within the next offset (further inside the Portlet), the drop will add the new Portlet to the existing row.

Finally, if the user drops outside both horizontal offsets (i.e., farther away from the edge), the drop will be interpreted as an attempt to add a new row—either above or below the current row, depending on the vertical position of the pointer.

**Flags**: IRW

---
## Attr: PortalLayout.canAcceptDrop

### Description
Drop is enabled for PortalLayouts by default. See [PortalLayout.dropTypes](#attr-portallayoutdroptypes) and [portalLayoutDrop](../kb_topics/portalLayoutDrop.md#kb-topic-drag-and-drop-behavior-within-portallayouts) for more information about PortalLayout drop behavior.

### Groups

- portalLayoutDrop

**Flags**: IRW

---
## Attr: PortalLayout.dropTypes

### Description
This property may be explicitly specified to restrict which [target dragTypes](Canvas.md#attr-canvasdragtype) may be dropped directly onto the PortalLayout. See the related [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes) property for how to restrict dropping portlets into a portalLayout and its sub-components (rows and columns).

If this property is not explicitly specified, drop behavior will be as follows when the user drops directly on the portalLayout outside any PortalColumns, or within the [PortalLayout.portletHDropOffset](#attr-portallayoutportlethdropoffset) of an existing column.

*   Drop will be allowed for targets with [dragType:"PortalColumn"](Canvas.md#attr-canvasdragtype). This allows the user to reorder portal columns by dragging using the column header.
*   If [PortalLayout.canAddColumns](#attr-portallayoutcanaddcolumns) is true, drop will also be allowed for other components that match the [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes) for the PortalLayout, if specified. If [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes) is unspecified, all other components may be dropped.  
    This allows the user to add columns to the portal layout by dropping components outside of any existing columns. If the dropped components are not instances of [Portlet](Portlet.md#class-portlet), a Portlet will be automatically created to contain them.  
    Note that if [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes) is specified, drop will be disallowed for any component whose dragType is not included in the portletDropTypes list, and is not `"PortalColumn"`

Developers may further restrict this behavior by specifying explicit dropTypes for the portalLayout. If you want to disallow adding new columns by dropping, but still have the user be able to add new columns with the [column menus](#attr-portallayoutshowcolumnmenus), set [PortalLayout.canAddColumns](#attr-portallayoutcanaddcolumns) to true and specify portalLayout.dropTypes as simply `["PortalColumn"]`.

### Groups

- portalLayoutDrop

### See Also

- [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes)

**Flags**: IR

---
## Attr: PortalLayout.removeEmptyColumns

### Description
Should empty columns automatically be removed when all portlets are removed from a column?

If true, when a portlet is removed from a column that didn't contain any other portlets, the column will be removed from the portalLayout. This is true if the portlet was removed via user action such as dragging the portlet into a different column, or if it was removed programatically, for example via a call to [PortalLayout.addPortlet](#method-portallayoutaddportlet) which specified a different column.

**Flags**: IRW

---
## Attr: PortalLayout.rowLayout

### Description
Automatically generated vertical [Layout](Layout.md#class-layout) used to create columns of [Portlets](Portlet.md#class-portlet) via [createAutoChild()](Class.md#method-classcreateautochild). Since this is an [AutoChild](../main.md#type-autochild), you can use rowLayoutDefaults and rowLayoutProperties to customize the layout used to contain the rows.

The rowLayout is the actual container for [rows](#attr-portallayoutrow) of [Portlets](Portlet.md#class-portlet). See [column](#attr-portallayoutcolumn) for the column as a whole, which may include a menu as well (depending on [showColumnMenus](#attr-portallayoutshowcolumnmenus)). If you want to style the columns as a whole, use columnDefaults or columnProperties, but if you want to style the layout that actually contains the rows, use rowLayoutDefaults or rowLayoutProperties.

### See Also

- [PortalLayout.rowLayout](#attr-portallayoutrowlayout)
- [PortalLayout.row](#attr-portallayoutrow)

**Flags**: A

---
## Attr: PortalLayout.columnSpacing

### Description
The space between portal columns.

To set spacing between portlets on a row in the same column, see [PortalLayout.portletHSpacing](#attr-portallayoutportlethspacing).

### Groups

- sizing

### See Also

- [PortalLayout.portletHSpacing](#attr-portallayoutportlethspacing)
- [PortalLayout.portletVSpacing](#attr-portallayoutportletvspacing)

**Flags**: IRW

---
## Attr: PortalLayout.canStretchColumnWidths

### Description
Controls whether the PortalLayout will stretch column widths, if needed to accommodate the width of [Portlets](Portlet.md#class-portlet). If set, columns will overflow their widths in order to accommodate the widths of their Portlets.

With the default setting of [Overflow](../main.md#type-overflow): auto, the PortalLayout as a whole will scroll horizontally if needed. Depending on the setting of [canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths), other columns may shrink to avoid overflow on the PortalLayout as a whole.

If `canStretchColumnWidths` is turned off, then individual rows will scroll horizontally in order to accommodate Portlets that are wider than their column width allows.

### Groups

- sizing

### See Also

- [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths)
- [PortalLayout.canResizePortlets](#attr-portallayoutcanresizeportlets)
- [Overflow](../main.md#type-overflow)

**Flags**: IRWA

---
## Attr: PortalLayout.portlet

### Description
[MultiAutoChild](../main.md#type-multiautochild) configuration for Portlets that will be automatically generated when the user drops a non-Portlet component into a PortalLayout.

Use standard autoChild pattern to customize the appearance and behavior of these standard generated portlet instances.

**Flags**: IRA

---
## Attr: PortalLayout.column

### Description
Automatically generated vertical [Layout](Layout.md#class-layout) used to create columns of [Portlets](Portlet.md#class-portlet) via [createAutoChild()](Class.md#method-classcreateautochild). Since this is an [AutoChild](../main.md#type-autochild), you can use columnDefaults and columnProperties to customize the columns.

The column includes a menu, if [showColumnMenus](#attr-portallayoutshowcolumnmenus) is true, and a [rowLayout](#attr-portallayoutrowlayout) which actually contains the [rows](#attr-portallayoutrow). Therefore, if you want to style the columns as a whole, use columnDefaults or columnProperties, but if you want to style the layout that contains the rows, use rowLayoutDefaults or rowLayoutProperties.

### See Also

- [PortalLayout.rowLayout](#attr-portallayoutrowlayout)
- [PortalLayout.row](#attr-portallayoutrow)

**Flags**: A

---
## Method: PortalLayout.willAcceptPortletDrop

### Description
This method will be invoked to determine whether a dragged [Portlet](Portlet.md#class-portlet) or other component can be dropped into this `PortalLayout` at the specified position.

The method will be called with the appropriate parameters from [Canvas.willAcceptDrop](Canvas.md#method-canvaswillacceptdrop) when the user attempts to drop within the PortalLayout or its subcomponents.

The default implementation acts like [Canvas.willAcceptDrop](Canvas.md#method-canvaswillacceptdrop), checking the [PortalLayout.dropTypes](#attr-portallayoutdroptypes) of the appropriate subcomponent, which will be derived from the [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes) by default.

This method may be overridden to control Portlet drop capabilities based on custom logic.

See [portalLayoutDrop](../kb_topics/portalLayoutDrop.md#kb-topic-drag-and-drop-behavior-within-portallayouts) for an overview of Portlet drop behaviors within a PortalLayout.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dragTarget | [Canvas](#type-canvas) | false | — | The [Portlet](Portlet.md#class-portlet), or other component, being dragged |
| colNum | [int](../main.md#type-int) | false | — | indicates the target column number for the portlet to be added to. |
| rowNum | [int](../main.md#type-int) | true | — | indicates the row number being dropped on within the target column. If this parameter is not passed, the user is attempting to add a new column by dropping outside any existing column. |
| dropPosition | [int](../main.md#type-int) | true | — | Drop position within an existing row. If this parameter is not passed, the user is attempting to add a new row by dropping above or below any existing row. |

### Returns

`[boolean](../main.md#type-boolean)` — true if the [Portlet](Portlet.md#class-portlet) or other component being dragged can be dropped on this PortalLayout, false otherwise

### Groups

- portalLayoutDrop

### See Also

- [Canvas.dragType](Canvas.md#attr-canvasdragtype)
- [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes)
- [PortalLayout.portletsChanged](#method-portallayoutportletschanged)

**Flags**: A

---
## Method: PortalLayout.setCanShrinkColumnWidths

### Description
Sets [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths) and reflows to reflect the new setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canShrink | [boolean](../main.md#type-boolean) | false | — | Whether columns can shrink to avoid overflowing the PortalLayout's width. |

### Groups

- sizing

### See Also

- [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths)
- [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths)

---
## Method: PortalLayout.getPortletArray

### Description
Returns a multi-level array of the [Portlets](Portlet.md#class-portlet) in this PortalLayout, where the first level corresponds to columns, the second to rows, and the third to Portlets within rows.

### Returns

`[Array of Array of Array of Portlet](#type-array-of-array-of-array-of-portlet)` — portlets

### See Also

- [PortalLayout.getPortlets](#method-portallayoutgetportlets)

---
## Method: PortalLayout.willAcceptDrop

### Description
This method has been overridden to support drag-reorder of PortalColumns, and adding of new rows by dropping directly on the PortalLayout, as described in [PortalLayout.dropTypes](#attr-portallayoutdroptypes)

### Returns

`[Boolean](#type-boolean)` — true if the widget object being dragged can be dropped on this widget, false if it cannot (and `drop()` should not bubble), null to permit `drop()` to bubble to parent elements

---
## Method: PortalLayout.setShowColumnMenus

### Description
Sets [PortalLayout.showColumnMenus](#attr-portallayoutshowcolumnmenus) and updates existing columns to reflect the new setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showMenus | [boolean](../main.md#type-boolean) | false | — | Whether to show column menus |

---
## Method: PortalLayout.removeColumn

### Description
Removes the specified column from this layout. All portlets displayed within this column will be destroyed when the column is removed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [int](../main.md#type-int) | false | — | column number to remove |

---
## Method: PortalLayout.getPortalPosition

### Description
Gets the position of the [Portlet](Portlet.md#class-portlet) within this PortalLayout. Returns null if the Portlet is not in this PortalLayout.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet for which to get the position |

### Returns

`[PortalPosition](#type-portalposition)` — the position of the Portlet

---
## Method: PortalLayout.portletRestored

### Description
Notification method called after a portlet has been restored to its normal place (after having been maximized). The method is called whether the restore is via user action or done programmatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which was restored |

### See Also

- [PortalLayout.willRestorePortlet](#method-portallayoutwillrestoreportlet)

---
## Method: PortalLayout.portletsChanged

### Description
Fires at initialization if the PortalLayout has any initial [portlets](Portlet.md#class-portlet), and then fires whenever portlets are added, removed or reordered.

### See Also

- [Layout.membersChanged](Layout.md#method-layoutmemberschanged)

---
## Method: PortalLayout.getNumColumns

### Description
Returns the current number of columns displayed in this PortalLayout.

### Returns

`[int](../main.md#type-int)` — numColumns

---
## Method: PortalLayout.willMinimizePortlet

### Description
Method called when a [Portlet](Portlet.md#class-portlet) in this PortalLayout is about to be minimized. Note that this method is only called when the user explicitly clicks on the portlet's [minimize button](Window.md#attr-windowshowminimizebutton) -- it is not called when programmatically minimizing a portlet via [minimize()](Window.md#method-windowminimize).

Return false to cancel the action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which will be minimized |

### Returns

`[boolean](../main.md#type-boolean)` — whether the action should proceed

### See Also

- [PortalLayout.portletMinimized](#method-portallayoutportletminimized)

---
## Method: PortalLayout.willMaximizePortlet

### Description
Method called when a [Portlet](Portlet.md#class-portlet) in this PortalLayout is about to be maximized. Note that this method is only called when the user explicitly clicks on the portlet's [maximize button](Window.md#attr-windowshowmaximizebutton) -- it is not called when programmatically maximizing a portlet via [maximize()](Window.md#method-windowmaximize).

Return false to cancel the action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which will be maximized |

### Returns

`[boolean](../main.md#type-boolean)` — whether the action should proceed

### See Also

- [PortalLayout.portletMaximized](#method-portallayoutportletmaximized)

---
## Method: PortalLayout.addColumn

### Description
Adds a new portal column to this layout at the specified position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [int](../main.md#type-int) | false | — | target position for the new column |

---
## Method: PortalLayout.setColumnOverflow

### Description
Sets [PortalLayout.columnOverflow](#attr-portallayoutcolumnoverflow) and updates existing columns to reflect the new setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| overflow | [Overflow](../main.md#type-overflow) | false | — | Overflow setting for columns |

### See Also

- [PortalLayout.columnOverflow](#attr-portallayoutcolumnoverflow)

---
## Method: PortalLayout.setColumnWidth

### Description
Sets the width of a column in the PortalLayout.

Note that this sets the intrinsic width of the column. Columns may also automatically stretch and shrink to accommodate the width of [Portlets](Portlet.md#class-portlet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNumber | [Integer](../main_2.md#type-integer) | false | — | Which column's width to set. |
| width | [Number](#type-number)|[String](#type-string) | false | — | How wide to make the column |

### See Also

- [Canvas.setWidth](Canvas.md#method-canvassetwidth)

---
## Method: PortalLayout.portletMinimized

### Description
Notification method called after a portlet has been minimized (whether by user action or programmatically).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which was minimized |

### See Also

- [PortalLayout.willMinimizePortlet](#method-portallayoutwillminimizeportlet)

---
## Method: PortalLayout.setCanAddColumns

### Description
Sets [PortalLayout.canAddColumns](#attr-portallayoutcanaddcolumns).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canAddColumns | [Boolean](#type-boolean) | false | — | The new value for `canAddColumns`. |

---
## Method: PortalLayout.setColumnPreventUnderflow

### Description
Sets [preventColumnUnderflow](#attr-portallayoutpreventcolumnunderflow) and reflows the layout to implement it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| preventColumnUnderflow | [boolean](../main.md#type-boolean) | false | — | Whether to stretch the last [Portlet](Portlet.md#class-portlet) in a column to fill the column's height. |

### Groups

- sizing

---
## Method: PortalLayout.setPortletDropTypes

### Description
Sets the [portletDropTypes](#attr-portallayoutportletdroptypes) to be applied when dropping [Portlets](Portlet.md#class-portlet) on this `PortalLayout`, or when dropping other components to be auto-wrapped in a [Portlet](Portlet.md#class-portlet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portletDropTypes | [Array of String](#type-array-of-string) | false | — | dropTypes to apply when dropping [Portlets](Portlet.md#class-portlet) |

### Groups

- dragdrop

### See Also

- [PortalLayout.portletDropTypes](#attr-portallayoutportletdroptypes)

---
## Method: PortalLayout.setCanStretchColumnWidths

### Description
Sets [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths) and reflows to reflect the new setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canStretch | [boolean](../main.md#type-boolean) | false | — | Whether columns can stretch to accommodate [Portlet](Portlet.md#class-portlet) widths. |

### Groups

- sizing

### See Also

- [PortalLayout.canStretchColumnWidths](#attr-portallayoutcanstretchcolumnwidths)
- [PortalLayout.canShrinkColumnWidths](#attr-portallayoutcanshrinkcolumnwidths)

---
## Method: PortalLayout.setColumnBorder

### Description
Sets the columnBorder for to the specified value and updates any drawn columns to reflect this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| columnBorder | [String](#type-string) | false | — | New border to show around columns |

---
## Method: PortalLayout.setCanResizeColumns

### Description
Set whether columns in this portalLayout are drag-resizable, and update any drawn columns to reflect this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canResize | [Boolean](#type-boolean) | false | — | Whether columns are drag-resizable |

### Groups

- sizing

### See Also

- [PortalLayout.canResizeColumns](#attr-portallayoutcanresizecolumns)

---
## Method: PortalLayout.setPreventUnderflow

### Description
Sets [preventUnderflow](#attr-portallayoutpreventunderflow) and reflows the layout to implement it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| preventUnderflow | [boolean](../main.md#type-boolean) | false | — | Whether to stretch the last column to fill the PortalLayout's width. |

### Groups

- sizing

---
## Method: PortalLayout.willClosePortlet

### Description
Method called when a [Portlet](Portlet.md#class-portlet) in this PortalLayout is about to be closed. This method is called before [Portlet.showCloseConfirmationMessage](Portlet.md#attr-portletshowcloseconfirmationmessage) is applied. Note that this method is called only when the user explicitly closes a Portlet. It is not called when programmatically removing a Portlet via [PortalLayout.removePortlet](#method-portallayoutremoveportlet).

Return false to cancel the action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which will be closed |

### Returns

`[boolean](../main.md#type-boolean)` — whether the action should proceed

### See Also

- [Portlet.showCloseConfirmationMessage](Portlet.md#attr-portletshowcloseconfirmationmessage)
- [PortalLayout.portletsChanged](#method-portallayoutportletschanged)

---
## Method: PortalLayout.setColumnSpacing

### Description
Sets [columnSpacing](#attr-portallayoutcolumnspacing) and reflows the layout to implement it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| spacing | [Integer](../main_2.md#type-integer) | false | — | The amount of space to apply between columns |

### Groups

- sizing

---
## Method: PortalLayout.portletsResized

### Description
Fires when [portlets](Portlet.md#class-portlet) or columns in this PortalLayout are resized. Note that this fires on a short delay -- otherwise, it would fire multiple times for each change, since most portlet size changes will affect multiple portlets. Does not fire when a portlet is [maximized](#method-portallayoutportletmaximized) or [restored](#method-portallayoutportletrestored).

---
## Method: PortalLayout.getDropPortlet

### Description
This method is called when the user drops components into the rows or columns of this PortalLayout.

Overriding this method allows you to modify drop behaviour when creating or reordering portlets via drag & drop. You can return the dragTarget for the standard behavior, or null to cancel the drop.

Otherwise, return the component you want to be dropped (as for [Layout.getDropComponent](Layout.md#method-layoutgetdropcomponent)). You will generally want to return a [Portlet](Portlet.md#class-portlet) or subclass. However, you can return any [Canvas](Canvas.md#class-canvas), and it will automatically be wrapped in a [Portlet](#attr-portallayoutportlet) if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dragTarget | [Canvas](#type-canvas) | false | — | drag target |
| colNum | [int](../main.md#type-int) | false | — | indicates the index of the column the portlet is being dropped on. Note that if a new column will be created (`rowNum` is `null`), then this will be the index of the new column, but it doesn't exist, yet. |
| rowNum | [Integer](../main_2.md#type-integer) | true | — | indicates the index of the row being dropped on. If the `rowNum` is `null`, a new column will be created to contain the portlet. |
| dropPosition | [Integer](../main_2.md#type-integer) | true | — | Drop position within an existing row. If the `dropPosition` is `null`, a new row will be created to contain the portlet. |

### Returns

`[Canvas](#type-canvas)` — drop-component or custom Portlet to embed in the portalLayout. Returning `null` will cancel the drop.

### See Also

- [PortalLayout.willAcceptPortletDrop](#method-portallayoutwillacceptportletdrop)
- [PortalLayout.portletsChanged](#method-portallayoutportletschanged)

---
## Method: PortalLayout.getPortlets

### Description
Returns a flat array of all the [Portlets](Portlet.md#class-portlet) in this PortalLayout.

### Returns

`[Array of Portlet](#type-array-of-portlet)` — portlets

### See Also

- [PortalLayout.getPortletArray](#method-portallayoutgetportletarray)

---
## Method: PortalLayout.setCanResizePortlets

### Description
Set whether the height and width of [Portlets](Portlet.md#class-portlet) should be drag-resizable, and update any drawn Portlets to reflect this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canResize | [Boolean](#type-boolean) | false | — | Whether drag-resizing the height and width of portlets is allowed |

### Groups

- sizing

### See Also

- [PortalLayout.canResizePortlets](#attr-portallayoutcanresizeportlets)

---
## Method: PortalLayout.addPortlet

### Description
Adds a [Portlet](Portlet.md#class-portlet) instance to this portalLayout in the specified position. PortalLayouts use columns to manage the positions of their portlets. Each column is a vertical stack containing a number of rows. By default a portlet within a column will take up the entire width of the column (so there is one portlet per row within the column), but developers may also place more than one portlet side-by-side on a row within a column - see the `positionInExistingRow` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Canvas](#type-canvas) | false | — | Portlet to add to this layout. If the component passed in is not an instance of [Portlet](Portlet.md#class-portlet) a [portlet auto child](#attr-portallayoutportlet) will be automatically created to hold the component and added to the layout at the appropriate position. |
| colNum | [Integer](../main_2.md#type-integer) | true | — | Column in which the Portlet should be added. If unspecified, portlet will be added to the first column. If specified, but the specified column does not exist, a column is automatically added at the specified colNum index. |
| rowWithinCol | [Integer](../main_2.md#type-integer) | true | — | Row-position within the specified column for this portlet. If unspecified defaults to zero - the portlet will be added to the top of the column. By default a new row will be added to the column for the portlet. Use the `positionInExistingRow` parameter to add the portlet to an existing row. |
| positionInExistingRow | [Integer](../main_2.md#type-integer) | true | — | Position within an existing row in the column. If this parameter is passed, this portlet will be added to the existing row at `rowWithinCol`, at the specified position. This allows developers to place multiple portlets side by side on a row within the column.  
If omitted a new row will be created in the column for the portlet. |

---
## Method: PortalLayout.setStretchColumnWidthsProportionally

### Description
Sets [PortalLayout.stretchColumnWidthsProportionally](#attr-portallayoutstretchcolumnwidthsproportionally) and reflows to reflect the new setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stretchProportionally | [boolean](../main.md#type-boolean) | false | — | Whether to stretch column widths proportionally |

### Groups

- sizing

### See Also

- [PortalLayout.stretchColumnWidthsProportionally](#attr-portallayoutstretchcolumnwidthsproportionally)

---
## Method: PortalLayout.willRestorePortlet

### Description
Method called when a [Portlet](Portlet.md#class-portlet) in this PortalLayout is about to be restored to its normal place (after having been [maximized](#method-portallayoutportletmaximized). Note that this method is only called when the user explicitly clicks on the portlet's [restore button](Window.md#attr-windowrestorebutton) -- it is not called when programmatically restoring a portlet via [restore()](Window.md#method-windowrestore).

Return false to cancel the action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which will be restored |

### Returns

`[boolean](../main.md#type-boolean)` — whether the action should proceed

### See Also

- [PortalLayout.portletRestored](#method-portallayoutportletrestored)

---
## Method: PortalLayout.setPortletHSpacing

### Description
Sets [portletHSpacing](#attr-portallayoutportlethspacing) and reflows the layout to implement it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| spacing | [Integer](../main_2.md#type-integer) | false | — | The amount of space to apply between portlets in a row |

### Groups

- sizing

---
## Method: PortalLayout.getColumnWidth

### Description
Gets the width of a column in the PortalLayout.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNumber | [int](../main.md#type-int) | false | — | Which column's width to get |

### Returns

`[int](../main.md#type-int)` — width

### See Also

- [Canvas.getWidth](Canvas.md#method-canvasgetwidth)

---
## Method: PortalLayout.portletMaximized

### Description
Notification method called after a portlet has been maximized (whether by user action or programmatically).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | the Portlet which was maximized |

### See Also

- [PortalLayout.willMaximizePortlet](#method-portallayoutwillmaximizeportlet)

---
## Method: PortalLayout.setPreventRowUnderflow

### Description
Sets [preventRowUnderflow](#attr-portallayoutpreventrowunderflow) and reflows the layout to implement it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| preventRowUnderflow | [boolean](../main.md#type-boolean) | false | — | Whether to stretch the last [Portlet](Portlet.md#class-portlet) in a row to to fill the row's width. |

### Groups

- sizing

---
## Method: PortalLayout.setCanResizeRows

### Description
Set whether vertical drag-resize of portlets within columns is allowed, and update any drawn columns to reflect this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canResize | [Boolean](#type-boolean) | false | — | Whether drag-resize of portlets within columns is allowed |

**Deprecated**

---
## Method: PortalLayout.setPortletVSpacing

### Description
Sets [portletVSpacing](#attr-portallayoutportletvspacing) and reflows the layout to implement it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| spacing | [Integer](../main_2.md#type-integer) | false | — | The amount of space to apply between rows |

### Groups

- sizing

---
## Method: PortalLayout.removePortlet

### Description
Removes a [Portlet](Portlet.md#class-portlet) which is currently rendered in this PortalLayout. Portlet will not be destroyed by default - if this is desired the calling code should do this explicitly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| portlet | [Portlet](#type-portlet) | false | — | portlet to remove |

---
