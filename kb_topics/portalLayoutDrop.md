# Drag and Drop behavior within PortalLayouts

[← Back to API Index](../main.md)

---

## KB Topic: Drag and Drop behavior within PortalLayouts

### Description
PortalLayouts are a special Layout subclass designed to contain [Portlet](../classes/Portlet.md#class-portlet) windows.

PortalLayouts support drag and drop behavior to add new Portlets to the layout and to reorganize the Portlets, as well as to reorder existing [columns](../classes/PortalLayout.md#attr-portallayoutcolumn).

Portlet drop behavior within a PortalLayout is enabled by default, and may be configured per portlet by setting [Portlet.canDragReposition](../classes/Window.md#attr-windowcandragreposition) and [Portlet.canDrop](../classes/Portlet.md#attr-portletcandrop). Developers wishing to restrict portlet drop capabilities by type may also set [Portlet.dragType](../classes/Portlet.md#attr-portletdragtype) and [PortalLayout.portletDropTypes](../classes/PortalLayout.md#attr-portallayoutportletdroptypes), or override [PortalLayout.willAcceptPortletDrop](../classes/PortalLayout.md#method-portallayoutwillacceptportletdrop) for custom restrictions.

Users may drop existing Portlets or any other droppable component into a portalLayout. If something other than a Portlet is dropped into a portalLayout, a [Portlet autoChild](../classes/PortalLayout.md#attr-portallayoutportlet) will automatically be created to contain it. Standard [autoChild](autoChildUsage.md#kb-topic-using-autochildren) configuration patterns may be used to customize these automatically created Portlets.

Users may add portlets to, or move portlets within a PortalLayout via the following interactions:

*   If [PortalLayout.canAddColumns](../classes/PortalLayout.md#attr-portallayoutcanaddcolumns) is true, users may add a new column to the PortalLayout by dropping a Portlet or other valid component directly onto the PortalLayout outside of any existing columns, or by dropping within the [PortalLayout.portletHDropOffset](../classes/PortalLayout.md#attr-portallayoutportlethdropoffset) of a column. The dropped component will be rendered inside the new column. This behavior can be turned off using [PortalLayout.canAcceptDrop](../classes/PortalLayout.md#attr-portallayoutcanacceptdrop) or setting [PortalLayout.dropTypes](../classes/PortalLayout.md#attr-portallayoutdroptypes) to explicitly disallow portlet drop.
*   The user may add a new row to a column by dropping into the [rowLayout within a column](../classes/PortalLayout.md#attr-portallayoutrowlayout). This behavior can be turned off by setting `canAcceptDrop` to false in the `portalLayout.rowLayoutProperties`.
*   The user may add a Portlet to an existing row by dropping within [PortalLayout.portletHDropOffset](../classes/PortalLayout.md#attr-portallayoutportlethdropoffset) of an existing Portlet in a row. This behavior can be turned off by setting `canAcceptDrop` to false in the defaults for the [row autoChildren](../classes/PortalLayout.md#attr-portallayoutrow) using `portalLayout.rowDefaults`

The actual component to be added to the PortalLayout on drop is returned by the [PortalLayout.getDropPortlet](../classes/PortalLayout.md#method-portallayoutgetdropportlet) method. This method may be overridden to change what components are added to the PortalLayout on drop.

By default when a user drags all the portlets out of a column, leaving it empty, the Column will automatically be removed from the Portlet. This behavior may be configured using [PortalLayout.removeEmptyColumns](../classes/PortalLayout.md#attr-portallayoutremoveemptycolumns).

### Related

- [PortalLayout.willAcceptPortletDrop](../classes/PortalLayout.md#method-portallayoutwillacceptportletdrop)
- [PortalLayout.canAcceptDrop](../classes/PortalLayout.md#attr-portallayoutcanacceptdrop)
- [PortalLayout.dropTypes](../classes/PortalLayout.md#attr-portallayoutdroptypes)

---
