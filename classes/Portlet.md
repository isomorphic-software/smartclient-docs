# Portlet Documentation

[← Back to API Index](../reference.md)

---

## Class: Portlet

*Inherits from:* [Window](Window.md#class-window)

### Description
Custom subclass of Window configured to be embedded within a [PortalLayout](PortalLayout.md#class-portallayout).

---
## Attr: Portlet.minWidth

### Description
Specifies a minimum width for the Portlet.

### See Also

- [Canvas.minWidth](Canvas.md#attr-canvasminwidth)

**Flags**: IRW

---
## Attr: Portlet.minHeight

### Description
Specifies a minimum height for the Portlet. The height of rows within a [PortalLayout](PortalLayout.md#class-portallayout) will be adjusted to take into account the minHeight of all the Portlets in that row.

### See Also

- [Canvas.minHeight](Canvas.md#attr-canvasminheight)

**Flags**: IRW

---
## Attr: Portlet.closeConfirmationMessage

### Description
Confirmation message to show the user when closing portlets if [Portlet.showCloseConfirmationMessage](#attr-portletshowcloseconfirmationmessage) is true.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: Portlet.rowHeight

### Description
If you set the rowHeight of a Portlet before adding it to a [PortalLayout](PortalLayout.md#class-portallayout), then the height will be used when creating the new row. If adding the Portlet to an existing row (or dragging it there), the Portlet's rowHeight will be used if the row's height has not already been specified. However, if you set the rowHeight of a Portlet after adding it to the PortalLayout, then the height of the entire row will always be adjusted to match.

You can also just specify [height](Canvas.md#attr-canvasheight) when initializing a Portlet, and it will be applied to the rowHeight when added to a PortalLayout. However, changing the Portlet's height after initialization will not affect the row.

Note that getting the rowHeight will indicate the rowHeight specified for this Portlet, not the actual height of the row it is in.

### Groups

- sizing

**Flags**: IRW

---
## Attr: Portlet.closeConfirmationDialogProperties

### Description
If specified, this properties block will be passed to [isc.confirm](isc.md#staticmethod-iscconfirm) as the properties parameter when the [Portlet.closeConfirmationMessage](#attr-portletcloseconfirmationmessage) is shown, allowing developers to customize the appear of the confirmation dialog (modifying its title, etc).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: Portlet.canDrop

### Description
Portlets have canDrop set to true to enable drag/drop reposition within the portalLayout

**Flags**: IRW

---
## Attr: Portlet.destroyOnClose

### Description
Whether to call [destroy()](Canvas.md#method-canvasdestroy) when closing the Portlet.

**Flags**: IRW

---
## Attr: Portlet.dragType

### Description
By default, [PortalLayout.portletDropTypes](PortalLayout.md#attr-portallayoutportletdroptypes) is set so that any component can be dragged into a [PortalLayout](PortalLayout.md#class-portallayout). If the component is not a [Portlet](#class-portlet), it will be automatically be wrapped in a newly created [Portlet](#class-portlet).

If you prefer to only allow real [Portlets](#class-portlet) to be dragged into a [PortalLayout](PortalLayout.md#class-portallayout), then you can set [PortalLayout.portletDropTypes](PortalLayout.md#attr-portallayoutportletdroptypes) to `["Portlet"]`, since `Portlet.dragType` defaults to `"Portlet"`.

if you want to allow some [Portlets](#class-portlet) to be dropped on a [PortalLayout](PortalLayout.md#class-portallayout) but not others, then you can specify a custom `dragType` for [Portlets](#class-portlet), and then set [PortalLayout.portletDropTypes](PortalLayout.md#attr-portallayoutportletdroptypes) as appropriate.

### Groups

- dragdrop

### See Also

- [Canvas.dragType](Canvas.md#attr-canvasdragtype)
- [PortalLayout.portletDropTypes](PortalLayout.md#attr-portallayoutportletdroptypes)

**Flags**: IRWA

---
## Attr: Portlet.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Portlet.showCloseConfirmationMessage

### Description
If true, [Portlet.closeConfirmationMessage](#attr-portletcloseconfirmationmessage) will be displayed before portlets are closed

**Flags**: IRW

---
## Attr: Portlet.height

### Description
If you initialize the height of a Portlet, then that height will be used as the Portlet's [rowHeight](#attr-portletrowheight) (if no rowHeight is set).

After initialization, the [PortalLayout](PortalLayout.md#class-portallayout) manages the height of Portlets. If you want to change the height, use [Portlet.setRowHeight](#method-portletsetrowheight).

### See Also

- [Portlet.rowHeight](#attr-portletrowheight)
- [Portlet.setRowHeight](#method-portletsetrowheight)

**Flags**: IRW

---
## Method: Portlet.getPortalPosition

### Description
Gets the position of the Portlet within its [PortalLayout](PortalLayout.md#class-portallayout). Returns null if the Portlet is not in a PortalLayout.

### Returns

`[PortalPosition](#type-portalposition)` — the position of the Portlet

---
## Method: Portlet.close

### Description
`close()` method overridden to show [Portlet.closeConfirmationMessage](#attr-portletcloseconfirmationmessage) to the user before removing the portlet from the PortalLayout via [PortalLayout.removePortlet](PortalLayout.md#method-portallayoutremoveportlet)

---
## Method: Portlet.setRowHeight

### Description
Sets the height of the Portlet's row (and, thus, indirectly sets the Portlet's own height). Use this instead of using [Portlet.setHeight](#method-portletsetheight) directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Number](#type-number) | false | — | new height |

### Groups

- sizing

---
## Method: Portlet.getPortalLayout

### Description
Gets the [PortalLayout](PortalLayout.md#class-portallayout) which encloses this Portlet (or null, if none).

### Returns

`[PortalLayout](#type-portallayout)` — the PortalLayout enclosing this Portlet

---
## Method: Portlet.setHeight

### Description
The height of a Portlet is managed by the [PortalLayout](PortalLayout.md#class-portallayout). If you want to change the Portlet's height, use [Portlet.setRowHeight](#method-portletsetrowheight) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Number](#type-number) | false | — | new height |

### Groups

- sizing

### See Also

- [Portlet.setRowHeight](#method-portletsetrowheight)
- [Portlet.rowHeight](#attr-portletrowheight)

---
## Method: Portlet.closeClick

### Description
Handles a click on the close button of this portlet. The default implementation calls [Portlet.close](#method-portletclose).

Override this method if you want other actions to be taken. Custom implementations may call `close()` to trigger the default behavior.

### Returns

`[Boolean](#type-boolean)` — Return false to cancel bubbling the click event

---
