# ActiveXControl Documentation

[← Back to API Index](../reference.md)

---

## Class: ActiveXControl

*Inherits from:* [BrowserPlugin](../reference.md#class-browserplugin)

### Description
ISC Abstraction for ActiveX controls

---
## Attr: ActiveXControl.codeBase

### Description
Specifies the URL from which to load the ActiveX control.

**Flags**: IR

---
## Attr: ActiveXControl.id

### Description
Sets the 'id' attribute on the object. If a name is not provided it will be auto-generated. Note that in general you don't need to set this. If you have a reference to your ISC ActiveX control object you can simply call [ActiveXControl.getPluginHandle](#method-activexcontrolgetpluginhandle) to get a handle to the element.

### See Also

- [ActiveXControl.getPluginHandle](#method-activexcontrolgetpluginhandle)
- [ActiveXControl.getPluginID](#method-activexcontrolgetpluginid)

**Flags**: IR

---
## Attr: ActiveXControl.params

### Description
A map of key/value pairs to pass to the Active X control as parameters.

**Flags**: IR

---
## Attr: ActiveXControl.uuid

### Description
Set this to the uuid of your Active X control - ISC will then generate the appropriate classID entry for you.

**Flags**: IR

---
## Attr: ActiveXControl.classID

### Description
This sets the value of the classID property on the object. This is meant to give you complete control over the generated HTML. In practice it may be more handy to set the uuid property on this object and let the classID be generated from that.

### See Also

- [ActiveXControl.uuid](#attr-activexcontroluuid)

**Flags**: IR

---
## Method: ActiveXControl.getPluginHandle

### Description
Returns a handle to the element for this ISC ActiveX control object.

### Returns

`[DOMElement](#type-domelement)` — pointer to the plugin element in the DOM

---
## Method: ActiveXControl.getPluginID

### Description
Returns the ID for this ISC ActiveX control object. If the `id` property was specified for the object, that will be used, otherwise the ID will be auto-generated.

### Returns

`[String](#type-string)` — the ID for this ISC ActiveX control object.

---
