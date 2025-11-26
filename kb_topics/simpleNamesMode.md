# Simple Names mode

[← Back to API Index](../reference.md)

---

## KB Topic: Simple Names mode

### Description
When SmartClient runs in "simple names" mode (the default), all ISC Classes and several global methods are installed as JavaScript global variables, that is, properties of the browser's "window" object. When simple names mode is disabled (called "portal mode"), the framework uses only the global variable: "isc" and global variables prefixed with "isc\_".

Portal mode is intended for applications which must integrate with fairly arbitrary JavaScript code written by third-party developers, and/or third party JavaScript frameworks, where it is important that each framework stays within it's own namespace.

In portal mode, all references to ISC classes and global functions must be prefixed with "isc.", for example:

```
 
      Canvas.create(addProperties({}, myDefaults))

 
```
would become
```
      isc.Canvas.create(isc.addProperties({}, myDefaults));

 
```
Portal mode is enabled by setting `window.isc_useSimpleNames = false` **before** SmartClient is loaded, generally inside the `<head>` element.

---
