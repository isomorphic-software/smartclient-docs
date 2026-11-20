# Handling concurrent edits in SmartClient DataSources

[← Back to API Index](../reference.md)

---

## KB Topic: Handling concurrent edits in SmartClient DataSources

### Description
How do SmartClient DataSources handle multiple users making changes to the same record?

Consider a scenario where two users - _userA_ and _userB_ - are logged into the same application and viewing the same set of records in a SmartClient application:

*   _userA_ makes a change to a record and [saves the edit](../classes/DynamicForm.md#method-dynamicformsavedata)
*   _userB_ then makes another change to the same record and saves their edit

By default SmartClient dataSources have simple "most recent edit wins" behavior, so the changes made by userB will be preserved in the dataSource permanent storage - though if [DataSource.sparseUpdates](../classes/DataSource_1.md#attr-datasourcesparseupdates) is true, any changes made by _userA_ to fields that were not explicitly edited by _userB_ will also be preserved.

In this case when _userA_ performs their first edit (before _userB_ has attempted a save), _userB_ will not see _userA_'s changes unless they explicitly re-fetch the data. Similarly, _userA_ will not see _userB_'s subsequent edit without a re-fetch.

In many applications this behavior is acceptable but there may be cases where users will need to see other users' updates as they occur, and simple "last edit wins" is not sufficient. There are 2 things you can do to make this more sophisticated:

**Broadcasting changes:**  
The [DataSource.updateCaches](../classes/DataSource_1.md#method-datasourceupdatecaches) method is a way to notify a DataSource that a change has occurred. It will update its client-side caches to reflect the change and databound components showing the record will be refreshed as appropriate.

Developers using the SmartClient server and [messaging](messaging.md#kb-topic-real-time-messaging) may use this feature to propagate changes from the server to the client.

See this [blog post](https://isomorphic.atlassian.net/wiki/spaces/Main/pages/525130/How+to+propagate+data+source+changes+to+all+clients+by+using+the+Real-Time+Messaging+Module) for details on this approach.  
_Note: The sample project in this post is a SmartGWT project rather than SmartClient project. This means the client-side code to handle the server response is written in Java rather than JavaScript - but the methodology directly translates to SmartClient JavaScript and should be easy to understand._

**Detecting concurrent edits:**  
Note that even if an application is using Realtime Messaging or some similar approach to notify users of external edits as soon as they occur, it is still possible to get concurrent edit attempts on the same record.

In our original scenario - if _userB_ hit their save button after _userA_ but before the server had processed _userA_'s request, _userB_'s edit would essentially be based on "stale" values.

The server can detect this because every "update" and "remove" request sent by a DataBound component carries [DSRequest.oldValues](../classes/DSRequest.md#attr-dsrequestoldvalues): the record as the client last saw it. The approach below, sometimes called optimistic concurrency or long transactions, compares what the client saw with what the row now holds, refuses the save when they differ, and hands back the current row so the user can decide what to do.

#### Server side: a version counter
Give the DataSource an integer field that the server increments on every update, and make the update's criteria the primary key plus that counter as the client last saw it. A save based on stale values then matches no row, and the server reports that with a status code of its own and the row as it now stands:
```
 <field name="version" type="integer" hidden="true"/>
 
```
The check is a few lines in a [custom DataSource](../classes/DataSource_1.md#attr-datasourceserverconstructor) that extends `SQLDataSource` (see [serverDataSourceImplementation](serverDataSourceImplementation.md#kb-topic-notes-on-server-side-datasource-implementations)) and overrides `executeUpdate()`, the method the framework calls for every update:
```
 public class VersionedDataSource extends SQLDataSource {

     // Any negative status the framework does not use: see the
     // STATUS_ constants on RPCResponse for the reserved ones
     public static final int STATUS_STALE_RECORD = -74;

     public DSResponse executeUpdate(DSRequest request) throws Exception {
         DataSource ds = request.getDataSource();
         String pkName = ds.getPrimaryKey();
         Map pkCriteria = request.getCriteria();
         Map oldValues = request.getOldValues();

         // oldValues must describe the row the update addresses, or a client could pass
         // another row's values to get past the check
         Object pk = pkCriteria.get(pkName);
         if (oldValues == null ||
             !String.valueOf(pk).equals(String.valueOf(oldValues.get(pkName))))
         {
             DSResponse error = new DSResponse();
             error.setStatus(DSResponse.STATUS_FAILURE);
             return error;
         }

         // Update only if the row still carries the version the client saw, and bump it
         Object version = oldValues.get("version");
         Map criteria = new HashMap();
         criteria.put(pkName, pk);
         criteria.put("version", version);
         request.setCriteria(criteria);
         long next = version == null ? 1 : Long.parseLong(version.toString()) + 1;
         request.setFieldValue("version", Long.valueOf(next));
         DSResponse response = super.executeUpdate(request);
         request.setCriteria(pkCriteria);

         // No row matched: somebody else saved first.  Return the row as it now stands,
         // fetched in the same transaction, with the status the client looks for
         if (response.getAffectedRows() == 0) {
             DSRequest current = new DSRequest();
             current.setDataSource(ds);
             current.setRPCManager(request.getRPCManager());
             current.setOperationType(DataSource.OP_FETCH);
             current.setCriteria(pkCriteria);
             DSResponse row = current.execute();
             row.setStatus(STATUS_STALE_RECORD);
             return row;
         }
         return response;
     }
 }
 
```
The same logic can be written as a [server script](../classes/OperationBinding.md#attr-operationbindingscript) on the update operationBinding, calling `dsRequest.execute()` where the class calls `super.executeUpdate()`.

Criteria set inside `executeUpdate()` reach the generated SQL as they are; the framework does not reduce them to the primary key, and `allowMultiUpdate` is not involved. The response carries the bumped version whichever [cacheSyncStrategy](../reference_2.md#type-cachesyncstrategy) the DataSource uses, so the client's next save of the same row compares against the new value.

Why a counter rather than the alternatives:

*   Using every field of `oldValues` as criteria works, but it is fragile: dates, decimals and nulls must survive a round trip through the client exactly, and a record taken from a grid may carry fields the server does not know.
*   A `modifierTimestamp` field is stored at whole-second precision unless [DataSourceField.storeMilliseconds](../classes/DataSourceField.md#attr-datasourcefieldstoremilliseconds) is set, so two saves within the same second are indistinguishable.
*   A counter is exact on every database, and the server owns it. The one rule is that every path that writes the row must go through the DataSource: an update made directly in the database, or through another DataSource on the same table, leaves the counter alone and is not detected.

#### Client side: let the user decide
A refused save arrives with the status chosen above and the current row in [DSResponse.data](../classes/DSResponse.md#attr-dsresponsedata). The user has three reasonable choices: keep editing, discard their changes, or save anyway over the other user's. "Save anyway" works by making the server's row the `oldValues` of the next save, so the version then matches.

In a [ListGrid](../classes/ListGrid_1.md#class-listgrid), [ListGrid.editFailed](../classes/ListGrid_2.md#method-listgrideditfailed) receives the response. For "save anyway", copy the server's values onto the grid's record, which is what the next save sends as `oldValues`, then save the row again:

```
 isc.ListGrid.create({
     dataSource: "supplyItemVersioned", canEdit: true, autoSaveEdits: false,
     editFailed : function (rowNum, colNum, newValues, oldValues, editCompletionEvent,
                            dsResponse)
     {
         if (dsResponse.status != -74) return;
         var grid = this, serverRow = dsResponse.data[0];
         isc.ask("Somebody else changed this record. Save your changes over theirs?",
             function (saveAnyway) {
                 if (!saveAnyway) {
                     grid.discardAllEdits([rowNum]);
                     // show the row as it now stands
                     grid.getDataSource().updateCaches({operationType: "update",
                                                        data: [serverRow]});
                 } else {
                     isc.addProperties(grid.getRecord(rowNum), serverRow);
                     grid.saveAllEdits([rowNum]);
                 }
             });
     }
 });
 
```
In a [DynamicForm](../classes/DynamicForm.md#class-dynamicform), pass [willHandleError](../classes/RPCRequest.md#attr-rpcrequestwillhandleerror) so the response reaches your callback, and for "save anyway" save again with the server's row as [DSRequest.oldValues](../classes/DSRequest.md#attr-dsrequestoldvalues):
```
 function saveForm(form, oldValues) {
     form.saveData(function (dsResponse) {
         if (dsResponse.status != -74) return;
         var serverRow = dsResponse.data[0];
         isc.ask("Somebody else changed this record. Save your changes over theirs?",
             function (saveAnyway) {
                 if (saveAnyway) saveForm(form, serverRow);
             });
     }, {willHandleError: true, oldValues: oldValues});
 }
 
```
Passing `null` as `oldValues` for the first save lets the form send the record it was given by [DynamicForm.editRecord](../classes/DynamicForm.md#method-dynamicformeditrecord), which is the normal behavior.

---
