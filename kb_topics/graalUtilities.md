# Graal Utilities

[← Back to API Index](../reference.md)

---

## KB Topic: Graal Utilities

### Description
Utility methods added to the `isc` global namespace when running under GraalJS. These provide convenient Java<->JavaScript type conversion, DSResponse creation, and logging without requiring `Java.type()` calls.

These methods are automatically available in server-side JavaScript when using `contextFiles="databinding"` or any other SmartClient module shortcut.

#### Type Conversion

*   [isc.toJavaMap](../classes/isc.md#classmethod-isctojavamap) / [isc.fromJavaMap](../classes/isc.md#classmethod-iscfromjavamap) - Object conversion
*   [isc.toJavaList](../classes/isc.md#classmethod-isctojavalist) / [isc.fromJavaList](../classes/isc.md#classmethod-iscfromjavalist) - Array conversion
*   [isc.hashMap](../classes/isc.md#classmethod-ischashmap) / [isc.concurrentHashMap](../classes/isc.md#classmethod-iscconcurrenthashmap) - Create Java Maps

#### DataSource Operations

*   [isc.dsResponse](../classes/isc.md#classmethod-iscdsresponse) - Create DSResponse with automatic type conversion
*   [isc.dsRequest](../classes/isc.md#classmethod-iscdsrequest) - Create DSRequest for direct Java execution

#### Logging

*   [isc.log](../classes/isc.md#classmethod-isclog) - Simple console output via System.out.println()
*   SmartClient logging (isc.Log.logWarn, this.logDebug, etc.) - Structured logging with categories and levels, also available under GraalJS

#### Other Utilities

*   [isc.nanoTime](../classes/isc.md#classmethod-iscnanotime) - High-resolution timing
*   [isc.fileExists](../classes/isc.md#classmethod-iscfileexists) / [isc.readFile](../classes/isc.md#classmethod-iscreadfile) - File operations
*   [isc.getConfig](../classes/isc.md#classmethod-iscgetconfig) - SmartClient server configuration
*   [isc.runProcess](../classes/isc.md#classmethod-iscrunprocess) - Execute external processes

### Related

- [isc.getGraalTypes](../classes/isc.md#classmethod-iscgetgraaltypes)
- [isc.toJavaMap](../classes/isc.md#classmethod-isctojavamap)
- [isc.toJavaList](../classes/isc.md#classmethod-isctojavalist)
- [isc.fromJavaMap](../classes/isc.md#classmethod-iscfromjavamap)
- [isc.fromJavaList](../classes/isc.md#classmethod-iscfromjavalist)
- [isc.fromJavaValue](../classes/isc.md#classmethod-iscfromjavavalue)
- [isc.javaBoolean](../classes/isc.md#classmethod-iscjavaboolean)
- [isc.dsResponse](../classes/isc.md#classmethod-iscdsresponse)
- [isc.log](../classes/isc.md#classmethod-isclog)
- [isc.nanoTime](../classes/isc.md#classmethod-iscnanotime)
- [isc.dsRequest](../classes/isc.md#classmethod-iscdsrequest)
- [isc.javaInteger](../classes/isc.md#classmethod-iscjavainteger)
- [isc.hashMap](../classes/isc.md#classmethod-ischashmap)
- [isc.concurrentHashMap](../classes/isc.md#classmethod-iscconcurrenthashmap)
- [isc.getSystemProperty](../classes/isc.md#classmethod-iscgetsystemproperty)
- [isc.setSystemProperty](../classes/isc.md#classmethod-iscsetsystemproperty)
- [isc.jacksonMapper](../classes/isc.md#classmethod-iscjacksonmapper)
- [isc.fileExists](../classes/isc.md#classmethod-iscfileexists)
- [isc.readFile](../classes/isc.md#classmethod-iscreadfile)
- [isc.getConfig](../classes/isc.md#classmethod-iscgetconfig)
- [isc.findInPath](../classes/isc.md#classmethod-iscfindinpath)
- [isc.runProcess](../classes/isc.md#classmethod-iscrunprocess)
- [isc.newUUID](../classes/isc.md#classmethod-iscnewuuid)
- [isc.now](../classes/isc.md#classmethod-iscnow)
- [isc.nowPlus](../classes/isc.md#classmethod-iscnowplus)
- [isc.isExpired](../classes/isc.md#classmethod-iscisexpired)
- [isc.failureResponse](../classes/isc.md#classmethod-iscfailureresponse)
- [isc.successResponse](../classes/isc.md#classmethod-iscsuccessresponse)
- [isc.executeDSRequest](../classes/isc.md#classmethod-iscexecutedsrequest)
- [isc.fetchOne](../classes/isc.md#classmethod-iscfetchone)
- [isc.updateRecord](../classes/isc.md#classmethod-iscupdaterecord)
- [isc.addRecord](../classes/isc.md#classmethod-iscaddrecord)

---
