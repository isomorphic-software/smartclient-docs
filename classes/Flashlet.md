# Flashlet Documentation

[← Back to API Index](../reference.md)

---

## Class: Flashlet

*Inherits from:* [BrowserPlugin](../reference.md#class-browserplugin)

### Description
ISC abstraction for Flashlets.

---
## Attr: Flashlet.pluginsPage

### Description
This attribute specifies the page the user should go to to get the plugin required to view this flashlet.

The default pluginsPage is: "http://www.macromedia.com/shockwave/download/index.cgi?P1\_Prod\_Version=ShockwaveFlash"

**Flags**: IR

---
## Attr: Flashlet.params

### Description
A map of key/value pairs to pass to the flashlet as parameters. Note that these will be set on the outer `<object>` element as well as the inner `<embed>` element.

**Flags**: IR

---
## Attr: Flashlet.classID

### Description
This attribute specifies the clsid of the outer `<object>` tag.

The default classID is: "clsid:D27CDB6E-AE6D-11cf-96B8-444553540000"

**Flags**: IR

---
## Attr: Flashlet.src

### Description
Location from which to load the Flashlet.

**Flags**: IR

---
## Attr: Flashlet.codeBase

### Description
This attribute specifies the minimum version of the flash player required to show this flashlet.

The default codeBase is: "http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=5,0,0,0"

**Flags**: IR

---
## Attr: Flashlet.name

### Description
Sets the 'name' attribute on the flashlet object. If a name is not provided it will be auto-generated. Note that in general you don't need to set this. If you have a handle to your ISC Flashlet object you can simply call [Flashlet.getPluginHandle](#method-flashletgetpluginhandle) to get a handle to the element.

### See Also

- [Flashlet.getPluginHandle](#method-flashletgetpluginhandle)

**Flags**: IR

---
## ClassMethod: Flashlet.flashAvailable

### Description
Is Shockwave Flash installed on this browser?

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if Flash is installed; `false` otherwise.

---
## ClassMethod: Flashlet.getFlashVersion

### Description
Which version of Flash is installed on this browser?

### Returns

`[number](#type-number)` — flash version number, or null if flash is not installed

---
## Method: Flashlet.setSrc

### Description
Sets the source file for the flash component

---
## Method: Flashlet.getPluginHandle

### Description
Returns a handle to the flashlet DOM element (valid only after the component has been drawn).

### Returns

`[DOMElement](#type-domelement)` — pointer to the plugin element in the DOM

**Flags**: A

---
