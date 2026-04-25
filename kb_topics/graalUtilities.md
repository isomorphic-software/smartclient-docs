# Graal Utilities

[← Back to API Index](../reference.md)

---

## KB Topic: Graal Utilities

### Description
Utility methods added to the `isc` global namespace when running under GraalJS. These provide convenient Java<->JavaScript type conversion, DSResponse creation, and logging without requiring `Java.type()` calls.

These methods are automatically available in server-side JavaScript when using `contextFiles="databinding"` or any other SmartClient module shortcut.

#### Type Conversion

*   [isc.toJavaMap](#classmethod-isctojavamap) / [isc.fromJavaMap](#classmethod-iscfromjavamap) - Object conversion
*   [isc.toJavaList](#classmethod-isctojavalist) / [isc.fromJavaList](#classmethod-iscfromjavalist) - Array conversion
*   [isc.hashMap](#classmethod-ischashmap) / [isc.concurrentHashMap](#classmethod-iscconcurrenthashmap) - Create Java Maps

#### DataSource Operations

*   [isc.dsResponse](#classmethod-iscdsresponse) - Create DSResponse with automatic type conversion
*   [isc.dsRequest](#classmethod-iscdsrequest) - Create DSRequest for direct Java execution

#### Logging

*   [isc.log](#classmethod-isclog) - Simple console output via System.out.println()
*   SmartClient logging (isc.Log.logWarn, this.logDebug, etc.) - Structured logging with categories and levels, also available under GraalJS

#### Other Utilities

*   [isc.nanoTime](#classmethod-iscnanotime) - High-resolution timing
*   [isc.fileExists](#classmethod-iscfileexists) / [isc.readFile](#classmethod-iscreadfile) - File operations
*   [isc.getConfig](#classmethod-iscgetconfig) - SmartClient server configuration
*   [isc.runProcess](#classmethod-iscrunprocess) - Execute external processes

### Related

- [isc.getGraalTypes](../classes/isc.md#staticmethod-iscgetgraaltypes)
- [isc.toJavaMap](../classes/isc.md#staticmethod-isctojavamap)
- [isc.toJavaList](../classes/isc.md#staticmethod-isctojavalist)
- [isc.fromJavaMap](../classes/isc.md#staticmethod-iscfromjavamap)
- [isc.fromJavaList](../classes/isc.md#staticmethod-iscfromjavalist)
- [isc.fromJavaValue](../classes/isc.md#staticmethod-iscfromjavavalue)
- [isc.javaBoolean](../classes/isc.md#staticmethod-iscjavaboolean)
- [isc.dsResponse](../classes/isc.md#staticmethod-iscdsresponse)
- [isc.log](../classes/isc.md#staticmethod-isclog)
- [isc.nanoTime](../classes/isc.md#staticmethod-iscnanotime)
- [isc.dsRequest](../classes/isc.md#staticmethod-iscdsrequest)
- [isc.javaInteger](../classes/isc.md#staticmethod-iscjavainteger)
- [isc.hashMap](../classes/isc.md#staticmethod-ischashmap)
- [isc.concurrentHashMap](../classes/isc.md#staticmethod-iscconcurrenthashmap)
- [isc.getSystemProperty](../classes/isc.md#staticmethod-iscgetsystemproperty)
- [isc.setSystemProperty](../classes/isc.md#staticmethod-iscsetsystemproperty)
- [isc.jacksonMapper](../classes/isc.md#staticmethod-iscjacksonmapper)
- [isc.fileExists](../classes/isc.md#staticmethod-iscfileexists)
- [isc.readFile](../classes/isc.md#staticmethod-iscreadfile)
- [isc.getConfig](../classes/isc.md#staticmethod-iscgetconfig)
- [isc.findInPath](../classes/isc.md#staticmethod-iscfindinpath)
- [isc.runProcess](../classes/isc.md#staticmethod-iscrunprocess)
- [isc.newUUID](../classes/isc.md#staticmethod-iscnewuuid)
- [isc.now](../classes/isc.md#staticmethod-iscnow)
- [isc.nowPlus](../classes/isc.md#staticmethod-iscnowplus)
- [isc.isExpired](../classes/isc.md#staticmethod-iscisexpired)
- [isc.failureResponse](../classes/isc.md#staticmethod-iscfailureresponse)
- [isc.successResponse](../classes/isc.md#staticmethod-iscsuccessresponse)
- [isc.executeDSRequest](../classes/isc.md#staticmethod-iscexecutedsrequest)
- [isc.fetchOne](../classes/isc.md#staticmethod-iscfetchone)
- [isc.updateRecord](../classes/isc.md#staticmethod-iscupdaterecord)
- [isc.addRecord](../classes/isc.md#staticmethod-iscaddrecord)

---
