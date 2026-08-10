# DefaultOperationTask Documentation

[← Back to API Index](../reference.md)

---

## Class: DefaultOperationTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
A server-side workflow task that executes the original incoming [DSRequest](../reference_2.md#object-dsrequest) via `dsRequest.execute()`. This is the declarative equivalent of calling `dsRequest.execute()` from a [ScriptTask](ScriptTask.md#class-scripttask) and is designed for processes that need to perform the default CRUD operation plus additional side-effect steps (cross-DataSource updates, notifications, etc.)

When used inside an [OperationBinding.process](OperationBinding.md#attr-operationbindingprocess), the task executes the same operation that would have run if no `process` were defined — including all server-side validators, Declarative Security constraints, and SQL/JPA generation. The resulting [DSResponse](DSResponse.md#class-dsresponse) is stored in the [Process.state](Process.md#attr-processstate) field named by [outputField](#outputfield).

**Values sync:** Before executing, the task copies all current `process.state.values` back into the original Java DSRequest. This means any modifications made by prior [ScriptTasks](ScriptTask.md#class-scripttask) (e.g. setting `process.state.values.status = "Approved"`) are included in the SQL INSERT/UPDATE automatically.

**Anti-recursion:** The original DSRequest has already passed through DMI dispatch, so `execute()` goes directly to the built-in DataSource CRUD — it does not re-enter the `process` operationBinding.

**Examples:**

CRUD with a side-effect (write an audit record after the update):

```
 <operationBinding operationType="update">
   <process>
     <Process startElement="doCRUD">
       <elements>
         <DefaultOperationTask ID="doCRUD"
             outputField="dsResponse"
             nextElement="audit"/>
         <DSAddTask ID="audit" dataSource="auditLog"
             ... />
       </elements>
     </Process>
   </process>
 </operationBinding>
 
```

Values sync — a [StateTask](StateTask.md#class-statetask) sets the status before DefaultOperationTask persists; the change is automatically included in the SQL INSERT:

```
 <operationBinding operationType="add">
   <process>
     <Process startElement="setStatus">
       <elements>
         <StateTask ID="setStatus"
             outputField="values.status"
             value="Approved"
             nextElement="persist"/>
         <DefaultOperationTask ID="persist"
             outputField="dsResponse"/>
       </elements>
     </Process>
   </process>
 </operationBinding>
 
```

### Groups

- serverProcess

### See Also

- [OperationBinding.process](OperationBinding.md#attr-operationbindingprocess)
- [serverProcess](../kb_topics/serverProcess.md#kb-topic-server-side-process-execution)

---
## Attr: DefaultOperationTask.failureElement

### Description
ID of the next element to execute if the default operation returns an error status. If unset and the operation fails, the process aborts with STATUS\_FAILURE.

**Flags**: IR

---
## Attr: DefaultOperationTask.outputField

### Description
Field in the [process state](Process.md#attr-processstate) where the [DSResponse](DSResponse.md#class-dsresponse) from the default operation is stored. Typically set to `"dsResponse"` so the process engine returns this response to the client.

### Groups

- taskIO

**Flags**: IR

---
## Attr: DefaultOperationTask.passThruOutput

### Description
(Boolean : false : IR)

**Flags**: IR

---
