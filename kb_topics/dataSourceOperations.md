# DataSource Operations

[← Back to API Index](../reference.md)

---

## KB Topic: DataSource Operations

### Description
A DataSource Operation is a type of [operation](operations.md#kb-topic-operations-overview) that acts on the set of stored objects represented by a [DataSource](../classes/DataSource.md#class-datasource), performing one of the basic actions that makes sense on a set of similar records: "fetch", "add", "update" or "remove". There is also a fifth DataSource Operation, "custom", which is intended for arbitrary server operations that are more complex than a fetch of some records, or an update to a single record.

Each DataSource operation has specific request and response data, for example, in the "fetch" DataSource operation, the request data is expected to be search criteria, and the response data is expected to be a list of matching DataSource records. Listed below are the request data and response data for each DataSource operation type, and what they mean.

DataSource records are represented on the client by a JavaScript Object, where each property in the Object maps a DataSource field name to the field value - hence the DataSource operations below are in essence a way of exchanging records from client to server and back.

If you are using [server-side data integration](serverDataIntegration.md#kb-topic-server-datasource-integration) with the SmartClient Java server, see the *Java Server Reference* for information about how DataSource Requests arrive on the server (specifically com.isomorphic.datasource.DSRequest) and how to provide responses (specifically com.isomorphic.datasource.DSResponse.setData()).

If you are using [client-side data integration](clientDataIntegration.md#kb-topic-client-side-data-integration) to directly consume services that use XML, JSON or other formats, see the "Editing and Saving" section of the [client-side data integration](clientDataIntegration.md#kb-topic-client-side-data-integration) topic.

**fetch**

*   Request data: filter criteria, as an Object
*   Response data: matching records, as an Array of Objects

**add**

*   Request data: new record, as an Object
*   Response data: new record as stored, as an Object or Array of one Object

**update**

*   Request data: primary keys of record to update, and new values (or just complete updated record), as an Object
*   Response data: new record as stored, as an Object or Array of one Object

**remove**

*   Request data: primary keys of record to delete, as an Object
*   Response data: minimally the primary keys of deleted record (can be complete record), as an Object or Array of one Object

**custom**

*   Request data: whatever the custom operation requires
*   Response data: custom operations can return whatever they like, including nothing. Custom operations are like RPC calls in this respect - the exchanged data is unstructured, so it is up to you to make sure the client and server agree. Note also that, because of this unstructured data exchange, cache synchronization does not work with custom operations.

If you need to do a **remove** with criteria rather than a primary key, the recommended approach is to do it as a **custom** operation so the intent is clear. You can also do it as a **remove**, but just use [DSRequest.oldValues](../classes/DSRequest.md#attr-dsrequestoldvalues) as the source for whatever criteria values you need. That covers everything except [AdvancedCriteria](../reference.md#object-advancedcriteria).

---
