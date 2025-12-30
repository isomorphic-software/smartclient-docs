# PrintProperties Documentation

[← Back to API Index](../reference.md)

---

## Attr: PrintProperties.includeControls

### Description
An array of Strings indicating the classNames of controls that should be specifically included when printing, even if a superclass is listed in [PrintProperties.omitControls](#attr-printpropertiesomitcontrols).

### Groups

- printing

**Flags**: IR

---
## Attr: PrintProperties.omitControls

### Description
An array of Strings indicating the classNames of controls that should be omitted from printing. By default, `omitControls` includes all button-based controls, menus and similar interactive controls that are typically useless in printed output.

All subclasses of the specified classes are also omitted.

See also [PrintProperties.includeControls](#attr-printpropertiesincludecontrols).

### Groups

- printing

**Flags**: IR

---
## Attr: PrintProperties.printForExport

### Description
If true, generates HTML for export.

Some components, specifically [DrawPane](DrawPane.md#class-drawpane) and [FacetChart](FacetChart.md#class-facetchart) on IE8 and earlier, need to generate different HTML for export versus in-browser print preview. When using [RPCManager.exportContent](RPCManager.md#classmethod-rpcmanagerexportcontent) the printForExport property is set to true automatically. If not using RPCManager.exportContent(), but the generated HTML will be sent for export, the `PrintProperties` passed to [Canvas.getPrintHTML](Canvas.md#method-canvasgetprinthtml) must have printForExport:true.

### Groups

- printing

**Flags**: IR

---
