# Client Only DataSources

[← Back to API Index](../reference.md)

---

## KB Topic: Client Only DataSources

### Description
For prototyping purposes, a "client-only" DataSource can be created that has no permanent storage and never contacts the server, instead using a set of test data to respond to requests in the same manner as a server-based DataSource might.

The client-side interface to a client-only DataSource is identical to a server-based DataSource, including asynchronous responses, so that a client-only DataSource can be replaced by a server-based DataSource without code changes. The only difference is that changes to records belonging to the DataSource persist only until the page is reloaded.

Client-only DataSources allow you to create a complete prototype application in an .html file that does not require a server.

The `clientOnly` property is specified to create a client-only DataSource, and the `cacheData` property should contain the test dataset, as an Array of Objects, one per DataSource record. For example:

```
   isc.DataSource.create({
       ID:"supplyItem",
       fields: ...,
       clientOnly:true,
       cacheData:[
          {itemName:"Pencil", cost:5.50},
          ...
       ]
   });
 
```
If you have existing test data in XML (see [Database Configuration](dbConfigTool.md#kb-topic-database-configuration) for expected format) and your client-only DataSource is defined in a .jsp file, you can use the XML->JS translation engine to populate the DataSource with data from XML, like so:
```
   isc.DataSource.create({
     ID:"solutions",
     fields: ...,
     clientOnly : true,
     cacheData : 
         <isomorphic:XML filename="shared/ds/test_data/solutions.data.xml"/>
   });
 
```
Another useful practice is to specify both the clientOnly DataSource and its test data in XML, so that the [Admin Console](adminConsole.md#kb-topic-admin-console) can later be used to import the DataSource and its test data into a SQL Database. An idiom for accomplishing this is:
```
   <isomorphic:loadDS name="solutions"/>
   isc.DataSource.getDataSource("solutions").addProperties({
     clientOnly : true,
     cacheData : 
        <isomorphic:XML filename="shared/ds/test_data/solutions.data.xml"/>
   });
 
```
Finally test data can be included directly in the clientOnly DataSource XML. An idiom for accomplishing this is:
```
 <DataSource ID="supplyItem">
   <fields>
       <field name="itemName" type="text" title="Item"/>
       <field name="SKU"      type="text" title="SKU"/>
   </fields>
   <cacheData>
       <Object>
           <itemName>name</itemName>
           <SKU>112233</SKU>
       </Object>
       ...
   </cacheData>
 </DataSource>
 
```
If you specify your DataSource as `clientOnly: true`, omit cacheData entirely, and provide either a [DataSource.dataURL](../classes/DataSource.md#attr-datasourcedataurl) or a `testFileName`, the DataSource will lazily make a one-time fetch against the specified data file the first time an operation is called on it. From then on, the DataSource will work against the local cache created from this initial request. This is a quick way to prototype against some test data that may eventually be returned from an arbitrary back-end.

Finally, it is possible to have a DataSource which initially fetches the entire dataset and performs all subsequent fetching locally, while still visiting the server to perform all other operations. See [DataSource.cacheAllData](../classes/DataSource.md#attr-datasourcecachealldata).

### Related

- [DataSource.clientOnly](../classes/DataSource.md#attr-datasourceclientonly)

---
