# LinkItem Documentation

[← Back to API Index](../reference.md)

---

## Class: LinkItem

*Inherits from:* [TextItem](TextItem.md#class-textitem)

### Description
A form item that displays a URL. In the default read-only mode ([canEdit](FormItem.md#attr-formitemcanedit) is `false`) the URL is shown as a link; in editable mode the URL is shown in a textbox.

The link to open is specified as the item value with [FormItem.setValue](FormItem.md#method-formitemsetvalue) or [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue). The link title defaults to the URL unless [LinkItem.linkTitle](#attr-linkitemlinktitle) is specified.

Additionally, a custom action can be triggered when the link is clicked: see [LinkItem.target](#attr-linkitemtarget) for details.

---
## Attr: LinkItem.readOnlyDisplay

### Description
If [canEdit](FormItem.md#attr-formitemcanedit) is set to `false`, how should this `LinkItem` be displayed to the user?

Link items are, by default, canEdit:false. Note that the link remains active regardless of the `readOnlyDisplay` setting.

### Groups

- appearance
- readOnly

### See Also

- [DynamicForm.readOnlyDisplay](DynamicForm.md#attr-dynamicformreadonlydisplay)

**Flags**: IRW

---
## Attr: LinkItem.disableIconsOnReadOnly

### Description
If [FormItem.canEdit](FormItem.md#attr-formitemcanedit) is set to false, should [icons](FormItem.md#attr-formitemicons) be disabled by default?

This may also be specified at the icon level. See [FormItemIcon.disableOnReadOnly](FormItemIcon.md#attr-formitemicondisableonreadonly).

### Groups

- formIcons

**Flags**: IRW

---
## Attr: LinkItem.linkTitle

### Description
Optional title HTML to display for this item's link. If unset, the `LinkItem`'s value (the URL) will be used for the link's title.

**Flags**: IRW

---
## Attr: LinkItem.target

### Description
By default, clicking a link rendered by this item opens it in a new browser window. You can alter this behavior by setting this property. The value of this property will be passed as the value to the `target` attribute of the anchor tag used to render the link.

If you set linkItem.target to "javascript", the default behaviour is to catch and consume mouse-clicks that would result in the link being followed. Instead, the [FormItem.click](FormItem.md#method-formitemclick) event is fired.

**Flags**: IRW

---
## Attr: LinkItem.iconVAlign

### Description
How should icons be aligned vertically for this form item.

### Groups

- formIcons

**Flags**: IRWA

---
## Method: LinkItem.setLinkTitle

### Description
Setter for [LinkItem.linkTitle](#attr-linkitemlinktitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [HTMLString](../reference.md#type-htmlstring) | false | — | new `linkTitle` HTML. |

---
