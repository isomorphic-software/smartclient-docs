# Server-Side Process Execution

[← Back to API Index](../reference.md)

---

## KB Topic: Server-Side Process Execution

### Description
**Server-Side Process Execution**

[OperationBinding.process](../classes/OperationBinding.md#attr-operationbindingprocess) allows a declarative [Process](../classes/Process.md#class-process) workflow to execute server-side as an alternative to [OperationBinding.script](../classes/OperationBinding.md#attr-operationbindingscript) or a [DMI](../reference_2.md#object-serverobject). The workflow is defined in the same XML format used by the [WorkflowEditor](#class-workfloweditor), making it visually editable by non-programmers.

**When to Use Each Approach**

| Approach | Best For | Editable? |
|---|---|---|
| process | Multi-step declarative logic: validate, branch, CRUD across DataSources, send email | Yes (WorkflowEditor) |
| script | Imperative logic: complex calculations, string manipulation, calling Java APIs directly | Code only |
| DMI (serverObject) | Heavy Java logic: third-party library integration, complex transactions, performance-critical paths | Code only |

**Input State**

The process receives automatic input state from the DSRequest:

*   `criteria`: Request criteria
*   `values`: Request values (add/update)
*   `oldValues`: Previous values (update)
*   `operationType`: "fetch", "add", "update", or "remove"
*   `dsName`: DataSource ID
*   `operationId`: The operationBinding's operationId
*   `auth.userId`: Authenticated user ID (from `DSRequest.getUserId()`)
*   `auth.roles`: User roles (from `DSRequest.getUserRoles()`)

These are available in [TaskInputExpressions](../reference_2.md#type-taskinputexpression) as `$criteria`, `$values`, etc.

**ServerDynamicCriteria in Process Workflows**

[DecisionTask](../classes/DecisionTask.md#class-decisiontask) and [MultiDecisionTask](../classes/MultiDecisionTask.md#class-multidecisiontask) criteria support the full [ServerDynamicCriteria](../reference_2.md#type-serverdynamiccriteria) syntax, including:

*   **Authentication context**: `auth.userId`, `auth.roles`
*   **Request context**: `context.operationType`, `context.operationId`
*   **Relational FK references**: dotted `_RelatedDS_._fieldName_` references are resolved automatically via the foreign key chain defined in the DataSource. For example, if an Order DS has `foreignKey="Customer.customerId"`, a criterion with `fieldName="Customer.creditStatus"` fetches the related Customer record and checks its `creditStatus` field
*   **Aggregation shorthand**: `_ChildDS_.#count` and `_ChildDS_._field_.#sum` compute aggregates over related child records. For example, if an Order DS has child LineItem records linked by FK, `LineItem.#count` resolves to the number of line items and `LineItem.amount.#sum` resolves to their total amount

**Output / Response**

The process produces a DSResponse via precedence:

1.  If `process.state.dsResponse` is set → used directly
2.  Else, output of last [DSRequestTask](../classes/DSRequestTask.md#class-dsrequesttask) that ran → its dsResponse.data
3.  Else → empty STATUS\_SUCCESS

**Error Handling**

If any task fails and has no [DSRequestTask.failureElement](../classes/DSRequestTask.md#attr-dsrequesttaskfailureelement), the process aborts immediately and returns STATUS\_FAILURE. If the operation participates in a transaction ([OperationBinding.autoJoinTransactions](#attr-operationbindingautojointransactions)), the transaction rolls back. When `autoJoinTransactions` is enabled, all [DS\*Tasks](../classes/DSRequestTask.md#class-dsrequesttask) in the process (including [DSAddTask](../reference.md#class-dsaddtask), [DSUpdateTask](../reference.md#class-dsupdatetask), [DSRemoveTask](../reference.md#class-dsremovetask), and [DefaultOperationTask](../classes/DefaultOperationTask.md#class-defaultoperationtask)) share the same database connection, so they commit or roll back as a unit.

**Server-Side Task Compatibility**

Compatible server-side tasks: [DefaultOperationTask](../classes/DefaultOperationTask.md#class-defaultoperationtask), [DecisionTask](../classes/DecisionTask.md#class-decisiontask), [MultiDecisionTask](../classes/MultiDecisionTask.md#class-multidecisiontask), [ScriptTask](../classes/ScriptTask.md#class-scripttask), [DSFetchTask](../reference.md#class-dsfetchtask), [DSAddTask](../reference.md#class-dsaddtask), [DSUpdateTask](../reference.md#class-dsupdatetask), [DSRemoveTask](../reference.md#class-dsremovetask), [StartProcessTask](../classes/StartProcessTask.md#class-startprocesstask), [EndProcessTask](../reference.md#class-endprocesstask), [StateTask](../classes/StateTask.md#class-statetask).

UI tasks (FormSetValuesTask, ShowHideTask, GridFetchDataTask, etc.) are NOT available and will log a warning if encountered.

**Performance**

Process execution uses server-side JavaScript context pooling. First invocation per pool slot incurs module loading overhead; subsequent invocations reuse the pre-loaded context with near-zero overhead beyond the actual DataSource operations.

**Example**

An Order DataSource with a foreign key to a Customer DataSource. On add, the process checks whether the customer's credit is approved (SDC relational FK reference) and rejects if not. If approved, a [ScriptTask](../classes/ScriptTask.md#class-scripttask) sets the status and a [DefaultOperationTask](../classes/DefaultOperationTask.md#class-defaultoperationtask) persists the record.

```
 <DataSource ID="order" serverType="sql">
   <fields>
     <field name="orderId" type="sequence"
            primaryKey="true"/>
     <field name="customerId" type="integer"
            foreignKey="customer.customerId"/>
     <field name="amount" type="float"/>
     <field name="status" type="text"/>
   </fields>

   <operationBindings>
     <operationBinding operationType="add"
         contextFiles="databinding"
         dataSources="customer">
       <process>
         <Process startElement="checkCredit">
           <elements>
             <DecisionTask ID="checkCredit"
                 nextElement="approve"
                 failureElement="reject">
               <criteria
                   fieldName="customer.creditStatus"
                   operator="equals"
                   value="approved"/>
             </DecisionTask>

             <StateTask ID="approve"
                 outputField="values.status"
                 value="Approved"
                 nextElement="persist"/>

             <DefaultOperationTask ID="persist"
                 outputField="dsResponse"/>

             <ScriptTask ID="reject">
               <script><![CDATA[
 process.state.dsResponse = {
     status: -1,
     data: "Customer credit not approved"
 };
               ]]></script>
             </ScriptTask>
           </elements>
         </Process>
       </process>
     </operationBinding>
   </operationBindings>
 </DataSource>
 
```

### Related

- [DSRequestTask](../classes/DSRequestTask.md#class-dsrequesttask)
- [DSFetchTask](../reference.md#class-dsfetchtask)
- [DSAddTask](../reference.md#class-dsaddtask)
- [DSUpdateTask](../reference.md#class-dsupdatetask)
- [DSRemoveTask](../reference.md#class-dsremovetask)
- [ScriptTask](../classes/ScriptTask.md#class-scripttask)
- [DecisionTask](../classes/DecisionTask.md#class-decisiontask)
- [MultiDecisionTask](../classes/MultiDecisionTask.md#class-multidecisiontask)
- [StateTask](../classes/StateTask.md#class-statetask)
- [StartProcessTask](../classes/StartProcessTask.md#class-startprocesstask)
- [SubProcessTask](../classes/SubProcessTask.md#class-subprocesstask)
- [UnexpectedErrorTask](../classes/UnexpectedErrorTask.md#class-unexpectederrortask)
- [EndProcessTask](../reference.md#class-endprocesstask)
- [SendEmailTask](../classes/SendEmailTask.md#class-sendemailtask)
- [SendSMSTask](../classes/SendSMSTask.md#class-sendsmstask)
- [DefaultOperationTask](../classes/DefaultOperationTask.md#class-defaultoperationtask)
- [OperationBinding.process](../classes/OperationBinding.md#attr-operationbindingprocess)
- [Process.dataSources](../classes/Process.md#attr-processdatasources)
- [ScriptTask.language](../classes/ScriptTask.md#attr-scripttasklanguage)
- [ScriptTask.dataSources](../classes/ScriptTask.md#attr-scripttaskdatasources)

### See Also

- [OperationBinding.process](../classes/OperationBinding.md#attr-operationbindingprocess)
- [OperationBinding.dataSources](../classes/OperationBinding.md#attr-operationbindingdatasources)
- [OperationBinding.contextFiles](../classes/OperationBinding.md#attr-operationbindingcontextfiles)
- [OperationBinding.script](../classes/OperationBinding.md#attr-operationbindingscript)
- [ServerDynamicCriteria](../reference_2.md#type-serverdynamiccriteria)
- [DecisionTask](../classes/DecisionTask.md#class-decisiontask)
- [MultiDecisionTask](../classes/MultiDecisionTask.md#class-multidecisiontask)
- [DefaultOperationTask](../classes/DefaultOperationTask.md#class-defaultoperationtask)
- [DSRequestTask](../classes/DSRequestTask.md#class-dsrequesttask)

---
