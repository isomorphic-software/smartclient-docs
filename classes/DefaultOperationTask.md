# DefaultOperationTask Documentation

[← Back to API Index](../reference.md)

---

## Class: DefaultOperationTask

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
A server-side workflow task that executes the original incoming [DSRequest](../reference_2.md#object-dsrequest) via `dsRequest.execute()`. This is the declarative equivalent of calling `dsRequest.execute()` from a [ScriptTask](ScriptTask.md#class-scripttask) and is designed for processes that need to perform the default CRUD operation plus additional side-effect steps (cross-DataSource updates, notifications, etc.)

When used inside an [OperationBinding.process](OperationBinding.md#attr-operationbindingprocess), the task executes the same operation that would have run if no `process` were defined — including all server-side validators, Declarative Security constraints, and SQL/JPA generation. The resulting [DSResponse](DSResponse.md#class-dsresponse) is stored in the [Process.state](Process.md#attr-processstate) field named by [outputField](#outputfield).

**Anti-recursion:** The original DSRequest has already passed through DMI dispatch, so `execute()` goes directly to the built-in DataSource CRUD — it does not re-enter the `process` operationBinding.

**Example:**

```
 <operationBinding operationType="update">
   <process>
     <Process startElement="doCRUD">
       <elements>
         <DefaultOperationTask ID="doCRUD"
             outputField="dsResponse"
             nextElement="audit"/>
         <DSAddTask ID="audit" dataSource="auditLog"
             ...
         />
       </elements>
     </Process>
   </process>
 </operationBinding>
 
```

### Groups

- serverProcess

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
