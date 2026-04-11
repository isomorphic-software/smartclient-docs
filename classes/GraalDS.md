# GraalDS Documentation

[← Back to API Index](../reference.md)

---

## Class: GraalDS

*Inherits from:* [DataSource](DataSource_1.md#class-datasource)

### Description
A DataSource subclass for use in server-side JavaScript running under GraalJS inside the Java VM. GraalDS provides direct, synchronous access to the SmartClient Server's DataSource machinery without HTTP round-trips.

GraalDS routes DataSource operations directly to Java `DSRequest.execute()`, enabling server-side JavaScript to use the familiar `isc.DataSource` API while benefiting from synchronous execution and direct Java interop.

**Environment Requirements**

GraalDS only functions when running under GraalJS in the Java VM. Attempting to use GraalDS in a browser or Node.js environment will log a warning and operations will fail. Use [GraalDS.isGraal](#classmethod-graaldsisgraal) to check whether the current environment supports GraalDS.

**Usage**

GraalDS can be used in two ways:

*   **Synchronous methods**: [GraalDS.fetchSync](#method-graaldsfetchsync), [GraalDS.addSync](#method-graaldsaddsync), [GraalDS.updateSync](#method-graaldsupdatesync), [GraalDS.removeSync](#method-graaldsremovesync) return data directly
*   **Standard DataSource API**: [DataSource.fetchData](DataSource_1.md#method-datasourcefetchdata), [DataSource.addData](DataSource_1.md#method-datasourceadddata), etc. work with callbacks. In the Graal server-side environment, callbacks always fire synchronously since Java `DSRequest.execute()` is synchronous

Example using synchronous methods:

```
 var ds = isc.GraalDS.get("supplyItem");
 var records = ds.fetchSync({category: "Office"});
 var newRecord = ds.addSync({itemName: "Pencil", category: "Office"});
 
```

**Java Type Conversion**

GraalDS automatically converts between JavaScript and Java types:

*   JavaScript objects <-> Java HashMap
*   JavaScript arrays <-> Java ArrayList
*   Primitive types pass through unchanged

Static utility methods [GraalDS.toJavaMap](#classmethod-graaldstojavamap) and [GraalDS.fromJavaMap](#classmethod-graaldsfromjavamap) are available for manual conversion when needed.

---
## Attr: GraalDS.isSynchronous

### Description
Flag indicating that this DataSource executes operations synchronously. In server-side GraalJS context, Java `DSRequest.execute()` is synchronous, so callbacks fire immediately. This property enables workflow tasks like [DSRequestTask](DSRequestTask.md#class-dsrequesttask) to detect synchronous DataSources and avoid callback-based async patterns that don't work correctly in server-side execution.

**Flags**: IR

---
## Attr: GraalDS.dataProtocol

### Description
GraalDS uses clientCustom protocol to intercept requests and execute them directly via Java DSRequest.

**Flags**: IR

---
## ClassMethod: GraalDS.toJavaList

### Description
Converts a JavaScript array to a Java ArrayList. Nested objects and arrays are recursively converted.

Note: The same functionality is available as [isc.toJavaList](isc.md#classmethod-isctojavalist).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsArray | [Array](#type-array) | false | — | JavaScript array to convert |

### Returns

`[Java.util.ArrayList](#type-javautilarraylist)` — Java ArrayList containing the converted data

---
## ClassMethod: GraalDS.isExpired

### Description
Checks if a Java Date is in the past.

Note: The same functionality is available as [isc.isExpired](isc.md#classmethod-iscisexpired).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| javaDate | [Java.util.Date](#type-javautildate) | false | — | Date to check |

### Returns

`[boolean](../reference.md#type-boolean)` — true if date is null or in the past

---
## ClassMethod: GraalDS.addRecord

### Description
Adds a record to a DataSource. Returns true on success.

Note: The same functionality is available as [isc.addRecord](isc.md#classmethod-iscaddrecord).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID |
| values | [Object](../reference.md#type-object) | false | — | Record values to add |

### Returns

`[boolean](../reference.md#type-boolean)` — true if add succeeded

---
## ClassMethod: GraalDS.get

### Description
Returns a GraalDS instance for the specified DataSource ID. If a DataSource with that ID already exists and is a GraalDS, returns it directly. Otherwise, creates a GraalDS wrapper that delegates to the existing DataSource definition.

This method allows server-side JavaScript to use any defined DataSource (SQL, generic, etc.) through the GraalDS interface for direct Java execution.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsID | [String](#type-string) | false | — | DataSource ID |

### Returns

`[GraalDS](#type-graalds)` — GraalDS instance for the specified DataSource

---
## ClassMethod: GraalDS.fromJavaMap

### Description
Converts a Java Map to a JavaScript object. Nested Maps and Lists are recursively converted to objects and arrays respectively.

Note: The same functionality is available as [isc.fromJavaMap](isc.md#classmethod-iscfromjavamap).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| javaMap | [Java.util.Map](#type-javautilmap) | false | — | Java Map to convert |

### Returns

`[Object](../reference.md#type-object)` — JavaScript object containing the converted data

---
## ClassMethod: GraalDS.now

### Description
Returns the current time as a Java Date object.

Note: The same functionality is available as [isc.now](isc.md#classmethod-iscnow).

### Returns

`[Java.util.Date](#type-javautildate)` — Current timestamp

---
## ClassMethod: GraalDS.toJavaMapViaJSON

### Description
Converts a JavaScript object to a Java Map using JSON serialization.

This alternative to [GraalDS.toJavaMap](#classmethod-graaldstojavamap) uses JSON.stringify() on the JavaScript side and Jackson ObjectMapper on the Java side. This approach may be faster for very large flat objects with simple types, but has limitations:

*   Requires Jackson library in classpath
*   Date objects are converted to ISO strings, not preserved as Date type
*   Cannot handle circular references
*   Functions and undefined values are omitted

For typical DataSource records, the manual iteration approach ([GraalDS.toJavaMap](#classmethod-graaldstojavamap)) is recommended as it handles all types correctly and benchmarks show it's faster for objects with fewer than ~100 fields.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsObject | [Object](../reference.md#type-object) | false | — | JavaScript object to convert |

### Returns

`[Java.util.Map](#type-javautilmap)` — Java Map containing the converted data, or null if Jackson unavailable

---
## ClassMethod: GraalDS.fromJavaList

### Description
Converts a Java List to a JavaScript array.

Note: The same functionality is available as [isc.fromJavaList](isc.md#classmethod-iscfromjavalist).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| javaList | [Java.util.List](#type-javautillist) | false | — | Java List to convert |

### Returns

`[Array](#type-array)` — JavaScript array containing the converted data

---
## ClassMethod: GraalDS.fromJavaValue

### Description
Converts any Java value to its JavaScript equivalent. Maps become objects, Lists become arrays, and primitives pass through unchanged.

Note: The same functionality is available as [isc.fromJavaValue](isc.md#classmethod-iscfromjavavalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | Java value to convert |

### Returns

`[Any](#type-any)` — JavaScript equivalent

---
## ClassMethod: GraalDS.executeDSRequest

### Description
Executes a DataSource operation directly via Java DSRequest.

Note: The same functionality is available as [isc.executeDSRequest](isc.md#classmethod-iscexecutedsrequest).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID |
| operationType | [String](#type-string) | false | — | Operation type: "fetch", "add", "update", "remove" |
| values | [Object](../reference.md#type-object) | true | — | Values for add/update operations |
| criteria | [Object](../reference.md#type-object) | true | — | Criteria for fetch/remove operations |
| operationId | [String](#type-string) | true | — | Custom operation ID |

### Returns

`[Com.isomorphic.datasource.DSResponse](#type-comisomorphicdatasourcedsresponse)` — Java DSResponse object

---
## ClassMethod: GraalDS.newUUID

### Description
Generates a new random UUID string.

Note: The same functionality is available as [isc.newUUID](isc.md#classmethod-iscnewuuid).

### Returns

`[String](#type-string)` — UUID string

---
## ClassMethod: GraalDS.successResponse

### Description
Creates a DSResponse with success status (0) and optional data.

Note: The same functionality is available as [isc.successResponse](isc.md#classmethod-iscsuccessresponse).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Object](../reference.md#type-object)|[Array](#type-array) | true | — | Response data (auto-converted to Java) |

### Returns

`[Com.isomorphic.datasource.DSResponse](#type-comisomorphicdatasourcedsresponse)` — Success DSResponse

---
## ClassMethod: GraalDS.nowPlus

### Description
Returns a Java Date representing the current time plus the specified milliseconds.

Note: The same functionality is available as [isc.nowPlus](isc.md#classmethod-iscnowplus).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| milliseconds | [Number](#type-number) | false | — | Milliseconds to add to current time |

### Returns

`[Java.util.Date](#type-javautildate)` — Future timestamp

---
## ClassMethod: GraalDS.updateRecord

### Description
Updates a record in a DataSource. Returns true on success.

Note: The same functionality is available as [isc.updateRecord](isc.md#classmethod-iscupdaterecord).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID |
| values | [Object](../reference.md#type-object) | false | — | Values to update (must include primary key) |

### Returns

`[boolean](../reference.md#type-boolean)` — true if update succeeded

---
## ClassMethod: GraalDS.failureResponse

### Description
Creates a DSResponse with failure status (-1) and an error message.

Note: The same functionality is available as [isc.failureResponse](isc.md#classmethod-iscfailureresponse).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | Error message |

### Returns

`[Com.isomorphic.datasource.DSResponse](#type-comisomorphicdatasourcedsresponse)` — Failure DSResponse

---
## ClassMethod: GraalDS.fetchOne

### Description
Fetches a single record from a DataSource matching the given criteria.

Note: The same functionality is available as [isc.fetchOne](isc.md#classmethod-iscfetchone).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID |
| criteria | [Object](../reference.md#type-object) | false | — | Criteria to match |

### Returns

`[Object](../reference.md#type-object)` — The first matching record, or null

---
## ClassMethod: GraalDS.fromJavaMapViaJSON

### Description
Converts a Java Map to a JavaScript object using JSON serialization.

This alternative to [GraalDS.fromJavaMap](#classmethod-graaldsfromjavamap) uses Jackson ObjectMapper to serialize the Java Map to JSON, then JSON.parse() on the JavaScript side.

Same limitations apply as [GraalDS.toJavaMapViaJSON](#classmethod-graaldstojavamapviajson) - Jackson must be available and certain types may not round-trip perfectly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| javaMap | [Java.util.Map](#type-javautilmap) | false | — | Java Map to convert |

### Returns

`[Object](../reference.md#type-object)` — JavaScript object containing the converted data, or null if Jackson unavailable

---
## ClassMethod: GraalDS.toJavaMap

### Description
Converts a JavaScript object to a Java HashMap using manual iteration. Nested objects and arrays are recursively converted to HashMap and ArrayList.

This is the recommended approach per GraalVM documentation. For an alternative using JSON serialization, see [GraalDS.toJavaMapViaJSON](#classmethod-graaldstojavamapviajson).

Note: The same functionality is available as [isc.toJavaMap](isc.md#classmethod-isctojavamap).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsObject | [Object](../reference.md#type-object) | false | — | JavaScript object to convert |

### Returns

`[Java.util.HashMap](#type-javautilhashmap)` — Java HashMap containing the converted data

---
## ClassMethod: GraalDS.log

### Description
Logs a message to the server console via System.out.println().

Note: The same functionality is available as [isc.log](isc.md#classmethod-isclog).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | Message to log |

---
## ClassMethod: GraalDS.isGraal

### Description
Returns true if the current JavaScript environment is GraalJS running inside the Java VM, meaning GraalDS operations will work.

### Returns

`[boolean](../reference.md#type-boolean)` — true if GraalJS environment is available

---
## Method: GraalDS.performDSOperationSync

### Description
Synchronously perform any DataSource operation, returning the full DSResponse object. Unlike the convenience methods like [GraalDS.fetchSync](#method-graaldsfetchsync) which return just the data, this method returns the complete response including status, startRow, endRow, and totalRows - useful for workflow tasks that need to check error status and handle pagination.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationType | [DSOperationType](../reference_2.md#type-dsoperationtype) | false | — | the type of operation to perform |
| data | [Record](#type-record)|[Criteria](../reference_2.md#type-criteria) | false | — | data for the operation (criteria for fetch, record for add/update/remove) |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional request properties like operationId, sortBy, startRow, endRow |

### Returns

`[DSResponse](#type-dsresponse)` — the full response object with status, data, startRow, endRow, totalRows

---
## Method: GraalDS.updateSync

### Description
Synchronously update a record in the DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record values to update (must include primary key) |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional request properties |

### Returns

`[Record](#type-record)` — the updated record as returned by the server, or null if failed

---
## Method: GraalDS.performCustomOperationSync

### Description
Synchronously perform a custom operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationId | [String](#type-string) | false | — | the operation ID |
| data | [Record](#type-record) | true | — | data to pass to the operation |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional request properties |

### Returns

`[Any](#type-any)` — the result data from the operation, or null if failed

---
## Method: GraalDS.removeSync

### Description
Synchronously remove a record from the DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record to remove (must include primary key) |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional request properties |

### Returns

`[Record](#type-record)` — the removed record, or null if failed

---
## Method: GraalDS.fetchSync

### Description
Synchronously fetch records from the DataSource.

Unlike [fetchData()](DataSource_1.md#method-datasourcefetchdata), this method blocks and returns the fetched data directly, making it convenient for server-side scripts that don't need async patterns.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional request properties |

### Returns

`[Array of Record](#type-array-of-record)` — the fetched records, or null if the operation failed

---
## Method: GraalDS.addSync

### Description
Synchronously add a record to the DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record to add |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional request properties |

### Returns

`[Record](#type-record)` — the added record as returned by the server, or null if failed

---
