# <isomorphic:loadDMIStubs>

[← Back to API Index](../main.md)

---

## KB Topic: <isomorphic:loadDMIStubs>

### Description
See [jspTags](../main.md#kb-topic-smartclient-jsp-tags)

_produces:_ JavaScript

Creates global bindings for all serverObjects defined in the `rpcBindings` section of the .app.xml file specified by the `ID` or `name` attribute of this tag. Once you've loaded your `rpcBindings` using this tag, you can call methods on the `ServerObjects` defined there directly. For example, you can load the example.app.xml (located in /shared/app directory of the webRoot of the SDK) like this:

```
 <isomorphic:loadDMIStubs ID="example"/>
 
```
Whereas using [DMI.call](../classes/DMI.md#classmethod-dmicall) you would have had to invoke the `getTimeStamp` method like this:
```
 DMI.call("example", "GetTimeStampDMI", "getTimeStamp", new Date(), "alert(data)";
 
```
Having loaded the stubs of the `example` .app.xml, you can then call `getTimeStamp` like this:
```
 GetTimeStampDMI.getTimeStamp(new Date(), "alert(data)");
 
```
or this:
```
 GetTimeStampDMI.getTimeStamp({
     arguments: [new Date()],
     callback: "alert(data)"
 });
 
```
or this:
```
 GetTimeStampDMI.call({
     methodName: "getTimeStamp",
     arguments: [new Date()],
     callback: "alert(data)"
 });
 
```
As with [DMI.call](../classes/DMI.md#classmethod-dmicall), the last argument must be the callback - if you don't want a callback, simply specify `null` as the callback. The name of the global binding created will be the same as the [ServerObject.ID](../classes/ServerObject.md#attr-serverobjectid) or the non-qualified name of the [ServerObject.className](../classes/ServerObject.md#attr-serverobjectclassname) (java namespace, if any, will be stripped).

**Tag Attributes:**

**ID or name**  
_value format_: String - name of .app.xml file to load (minus the .app.xml extension)  
_default value_: NONE

This attribute specifies the name of the file that contains the rpcBindings to load. UI files are located in `[webroot]/shared/app` by default. This location is changeable in [\[webroot\]/WEB-INF/classes/server.properties](server_properties.md#kb-topic-serverproperties-file) by setting the config parameter `project.apps` to the directory where your .app.xml files are located. We recommend that for prototyping, at least, you use the default directory.

### See Also

- [DMI](../classes/DMI.md#class-dmi)

---
