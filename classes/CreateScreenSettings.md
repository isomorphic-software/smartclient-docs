# CreateScreenSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: CreateScreenSettings.verifyAsError

### Description
Enable [verifyAsError](RPCManager.md#classattr-rpcmanagerverifyaserror) behavior only for requests using these settings.

### See Also

- [CreateScreenSettings.verifyAsError](#attr-createscreensettingsverifyaserror)
- [LoadProjectSettings.verifyAsError](LoadProjectSettings.md#attr-loadprojectsettingsverifyaserror)

**Flags**: IRW

---
## Attr: CreateScreenSettings.htmlElement

### Description
Simplifies integrating a screen with an existing JavaScript app. Does the following:

*   Sets [CreateScreenSettings.suppressAutoDraw](#attr-createscreensettingssuppressautodraw): true
*   Sets [Canvas.htmlElement](Canvas.md#attr-canvashtmlelement) of the screen's top widget to the DOM element
*   Sets the screen's top widget to have [Canvas.position](Canvas.md#attr-canvasposition): "relative"
*   Draws the screen by calling [Canvas.draw](Canvas.md#method-canvasdraw) on the top widget

If you need to apply additional, custom configuration, for example setting [Canvas.htmlPosition](Canvas.md#attr-canvashtmlposition), then instead of using this property, you can call [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen) with [CreateScreenSettings.suppressAutoDraw](#attr-createscreensettingssuppressautodraw): true, and then manually configure and draw the screen:
```
     var screen = isc.RPCManager.createScreen("My Screen", {suppressAutoDraw: true});
     screen.setHtmlElement(element);
     screen.setHtmlPosition("replace");
     screen.position = "relative";
     screen.draw();
 
```

**Flags**: IR

---
## Attr: CreateScreenSettings.clobberDataSources

### Description
Should DataSources referenced by the screen clobber existing, globally-bound DataSources on the client when the screen is created? The default of false means that any DataSources defined in the screen will be discarded if they collide with existing, globally-bound DataSources.

Note that here we consider a DataSource to be "globally bound" if it can be retrieved by ID using the method [DataSource.get](DataSource.md#classmethod-datasourceget), regardless of whether it's actually bound to the browser `window` object.

**Flags**: IRW

---
## Attr: CreateScreenSettings.componentSubstitutions

### Description
Defines the map of new widget [ids](Class.md#method-classgetid) to existing class instances, or to new instances that will be of a different class. A substituted class instance is returned immediately from [Class.create](Class.md#classmethod-classcreate) without modification. Otherwise, the constructor for the new instance is run, but targeting the substituted class rather than the original.

Note that where we return an existing instance, not even its [Canvas.ID](Canvas.md#attr-canvasid) will be changed. An alternative is programmtic replacement using [Layout.replaceMember](Layout.md#method-layoutreplacemember).

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

**Flags**: IR

---
## Attr: CreateScreenSettings.suppressAutoDraw

### Description
If true, prevents any screen from being drawn when it's created, even if there's an explicit [Canvas.autoDraw](Canvas.md#attr-canvasautodraw):true setting on it.

**Flags**: IR

---
## Attr: CreateScreenSettings.dataContext

### Description
[DataContext](../reference.md#object-datacontext) that will be provided to the top-level component as [dataContext](Canvas.md#attr-canvasdatacontext) in the screen.

To understand how `dataContext` is used to automatically populate [DataBoundComponents](../reference.md#interface-databoundcomponent), see [Canvas.autoPopulateData](Canvas.md#attr-canvasautopopulatedata).

### Groups

- dataContext

**Flags**: IR

---
## Attr: CreateScreenSettings.verifyComponents

### Description
Enables verification that the created screen contains a component having a `localId` equal to the given key, and that it is an instance (or subclass) if the key's value. Example:
```
   {'customerListGrid: 'ListGrid'}
 
```
You may verify presence and type of Tabs, SectionStackSections, and FormItems by providing their names following the parent component's id in dot-separated notation. Example:
```
   {
     'mainTabSet.customersTab': 'ImgTab',
     'mainSectionStack.customersSection': 'SectionHeader',
     'customerDetailsForm.customerNameItem': 'TextItem'
   }
 
```
Findings are always reported to the console, and may also be presented to the user with a warning dialog by setting [CreateScreenSettings.verifyAsError](#attr-createscreensettingsverifyaserror) or [RPCManager.verifyAsError](RPCManager.md#classattr-rpcmanagerverifyaserror).

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

**Flags**: IR

---
## Attr: CreateScreenSettings.allowPlaceholders

### Description
Should [Placeholders](Placeholder.md#class-placeholder) be rendered as placeholders? If property is not set actual components are created instead of the Placeholders.

**Flags**: IR

---
## Attr: CreateScreenSettings.classSubstitutions

### Description
Maps class names of widgets in the screen to new class names, so that if a widget would normally be constructed as an instance of a class, and that class is in the map, it's instead constructed as an instance of the new class.

### See Also

- [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen)

**Flags**: IR

---
