# Process Documentation

[← Back to API Index](../reference.md)

---

## Class: Process

### Description
A instance of Process represents a stateful process executing a series of Tasks, which may be:

*   user interactions
*   calls to DataSources (hence: any database or web service)
*   arbitrary code
*   other Processes

A Process is _stateful_ in the sense that it maintains [state](#attr-processstate) across the different tasks that are executed. This allows you to maintain context as you walk a user through a multi-step business process in your application, which may involve multiple operations on multiple entities. Each Task that executes can use the Process state as inputs, and can output a result which is stored in the Process state - see [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

A Process can have multiple branches, choosing the next Task to execute based on [Criteria](../reference_2.md#type-criteria) - see [DecisionTask](DecisionTask.md#class-decisiontask) and [MultiDecisionTask](MultiDecisionTask.md#class-multidecisiontask).

Because a Process may return to a previous Task in various situations, the data model of a Process is strictly speaking a _graph_ (a set of nodes connected by arbitary interlinks). However, most processes have sequences of several tasks in a row, and the definition format allows these to be represented as simple Arrays called "sequences", specified via [Process.sequences](#attr-processsequences). This reduces the need to manually specify IDs and interlinks for Tasks that simply proceed to the next task in a sequence.

Processes follow all the standard rules for encoding as [componentXML](../kb_topics/componentXML.md#kb-topic-component-xml), however, note that the `<Process>` tag allows any kind of [ProcessElement](ProcessElement.md#class-processelement) (tasks, decisions and sequences) to appear as a direct subelement of the `<Process>` tag without the need for an intervening `<elements>` or `<sequences>` tag. The example below demonstrates this shorthand format.

```
 <Process ID="processId">
     <DSRequestTask ID="dsRequestTaskId" nextElement="sequenceId" ..>
         <inputFieldList>
             <value>order.countryName</value>
         </inputFieldList>
         <outputFieldList>
             <value>order.countryName</value>
             <value>order.continent</value>
         <outputFieldList>
     </DSRequestTask>
     <sequence ID="sequenceId" >
         <StateTask ../>
         <StateTask ../>
         <StateTask ../>
         <StateTask nextElement="userTaskId" ../>
     </sequence>
     <UserTask ID="userTaskId" ../>
     ...
 </Process>
 
```
_**NOTE:** you must load the standard DataBinding module before you can use `Process`._

---
## ClassAttr: Process.defaultErrorHandlingEnabled

### Description
Framework-wide switch for the [Process-level default error task](#attr-processerrortask) fallback: when a task fails with no [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement) of its own and its owning Process (or an ancestor Process, if invoked as a [sub-process](SubProcessTask.md#class-subprocesstask)) has no explicit [Process.errorTask](#attr-processerrortask) either, a task failure used to always abort the Process straight to [finished()](#method-processfinished) with empty state/output - indistinguishable from a genuinely successful, empty result. With this flag at its default of `true`, that case now instead runs a default [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask) (see [Process.getDefaultErrorTask](#classmethod-processgetdefaulterrortask)), which routes the failure through [Process.fail](#method-processfail) instead - so [Process.failed](#method-processfailed) fires, not `finished()`, giving a real, distinguishable "did not complete successfully" signal for any Workflow that does not explicitly configure otherwise.

Set this to `false` to restore that prior behavior framework-wide (a task failure with no `failureElement` and no `errorTask` anywhere in the ancestry silently reaches `finished()`). A single Process can also opt out on its own via `errorTask: false`, without affecting any other Process.

**Flags**: IRW

---
## ClassAttr: Process.decisionPlaceholderSelection

### Description
Value of `failureElement` in various [tasks](ProcessElement.md#class-processelement) to indicate a placeholder is being used. Also applies to [DecisionBranch.targetTask](DecisionBranch.md#attr-decisionbranchtargettask) and [MultiDecisionTask.defaultElement](MultiDecisionTask.md#attr-multidecisiontaskdefaultelement).

**Flags**: IR

---
## ClassAttr: Process.suppressDefaultErrorPopupWhenHandled

### Description
Framework-wide switch controlling whether a DataSource-operation task's (or [SendEmailTask](SendEmailTask.md#class-sendemailtask)/[SendSMSTask](SendSMSTask.md#class-sendsmstask)/[FormSaveDataTask](FormSaveDataTask.md#class-formsavedatatask)'s) automatic [runDefaultErrorHandling()](RPCManager.md#classmethod-rpcmanagerrundefaulterrorhandling) dialog/ report fires when the failure is ALSO about to be routed to a [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement) or the owning Process's effective [Process.errorTask](#attr-processerrortask). Previously this raw, generic error surface always fired unconditionally, in addition to whatever failureElement/errorTask handling ran right afterward - visible, for example, as both a modal `isc.warn()`\-style dialog AND a graceful toast notification for the exact same single failure.

With this flag at its default of `true`, the dialog/report is skipped whenever the failing task resolves a real failure target - an explicit `failureElement`, the literal `"next"` continuation sentinel (meaning "resume as if nothing failed" - popping a dialog anyway would contradict that explicit choice), or the Process-level default error task (see [Process.defaultErrorHandlingEnabled](#classattr-processdefaulterrorhandlingenabled)) - i.e. whenever SOMETHING will visibly respond to the failure. It still fires when nothing will: no `failureElement`, and no effective `errorTask` anywhere in the Process's ancestry.

Set to `false` to restore the unconditional prior behavior framework-wide (the raw dialog always fires, regardless of `failureElement`/`errorTask`). Does not affect [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask)'s OWN, separate, classification-aware dialog ([Process.classifyError](#classmethod-processclassifyerror)) - that one already only shows for an "unexpected" classification, which is exactly the kind of narrower, smarter judgment this flag defers to instead of duplicating; as a direct consequence, suppressing the raw, unconditional dialog here also eliminates what used to be a genuine double-dialog for an unhandled failure that falls through to the default `UnexpectedErrorTask` (the raw dialog, immediately followed by `UnexpectedErrorTask`'s own).

**Flags**: IRW

---
## Attr: Process.currentTask

### Description
The task that is currently being executed by this process, or `null` when no task is running. Populated by [Process.start](#method-processstart) immediately before each call to [ProcessElement.executeElement](ProcessElement.md#method-processelementexecuteelement) and remains set until either (a) the task completes synchronously and the loop advances, or (b) the task completes asynchronously and a subsequent [Process.start](#method-processstart) invocation picks up the next task and overwrites the pointer. A fully-finished process clears it back to `null`.

This is the authoritative "what is running right now" pointer for code that needs to inspect the active task from outside the execution call stack - most notably CoT prompt assembly, which uses it to resolve task-scoped prompt fragments against the correct [CoTTask](CoTTask.md#class-cottask). Application code should treat it as read-only.

**Flags**: IR

---
## Attr: Process.state

### Description
Current state of a process. As with Records in general, any field of a Record may contain a nested Record or Array of Records, so the process state is essentially a hierarchical data structure.

#### Transient state
In addition to the explicit process state there is a "transient state." The transient state represents the complete output of each of the last tasks of each type within the current process execution. This allows easy reference to the previous task output with [taskInputExpressions](../reference_2.md#type-taskinputexpression).

**Flags**: IRW

---
## Attr: Process.defaultProcessConstructor

### Description
Name of the default Process subclass to use when auto-constructing plain Objects that are detected as Processes (see heuristic on [Process.defaultTaskConstructor](#attr-processdefaulttaskconstructor))

**Flags**: IR

---
## Attr: Process.inputFields

### Description
Shorthand alternative to [Process.inputDS](#attr-processinputds): a list of [DataSourceField](../reference_2.md#object-datasourcefield) definitions the engine compiles into a temporary validation DataSource on demand.

See [processIO](../kb_topics/processIO.md#kb-topic-process-input-and-output-schema).

**Flags**: IR

---
## Attr: Process.sequences

### Description
Sequences of ProcessElements. By defining a sequences of elements you can make the [ProcessElement.nextElement](ProcessElement.md#attr-processelementnextelement) implicit.

For a simple sequence of tasks, consider using [Process.tasks](#attr-processtasks) instead.

You do not have to explicitly create a [ProcessSequence](../reference.md#class-processsequence), you can instead use the shorthand:

```
 isc.Process.create({
     startElement:"firstSequence", 
     sequences: [
         { ID:"something", elements: [ ... ] },
         { ID:"somethingElse", elements: [ ... ] },
         ...
     ]
     ...
 });
 
```
.. this is equivalent to ..
```
 isc.Process.create({
     startElement:"firstSequence", 
     sequences: [
         isc.ProcessSequence.create({ 
              ID:"something", 
              elements: [ ... ] 
         }),
         isc.ProcessSequence.create({ 
              ID:"somethingElement", 
              elements: [ ... ] 
         }),
         ...                           
     ]
     ...
 });
 
```

**Flags**: IR

---
## Attr: Process.dataSources

### Description
Comma-separated list of DataSource IDs to pre-load when this process runs server-side (inside an [OperationBinding.process](OperationBinding.md#attr-operationbindingprocess)). The listed DataSources become available to all [ScriptTasks](ScriptTask.md#class-scripttask) in the process as DataSource instances and same-named local variables.

This is the process-level equivalent of [OperationBinding.dataSources](OperationBinding.md#attr-operationbindingdatasources); it scopes the pre-load to this process definition rather than the enclosing operationBinding. Individual ScriptTasks can list additional DataSources via [ScriptTask.dataSources](ScriptTask.md#attr-scripttaskdatasources).

DataSources already listed on the operationBinding or referenced directly in DS\*Task `dataSource` attributes do not need to be listed here.

This attribute has no effect in client-side workflows.

### Groups

- serverProcess

### See Also

- [OperationBinding.dataSources](OperationBinding.md#attr-operationbindingdatasources)
- [ScriptTask.dataSources](ScriptTask.md#attr-scripttaskdatasources)

**Flags**: IR

---
## Attr: Process.outputDS

### Description
Optional [DataSource](DataSource_1.md#class-datasource) that describes and validates the final output this Process produces on successful completion. May be a full DataSource definition, an existing instance, or the global ID of a registered DataSource.

See [processIO](../kb_topics/processIO.md#kb-topic-process-input-and-output-schema). When set, a [SubProcessTask](SubProcessTask.md#class-subprocesstask) caller references fields on this schema via `$output.`<fieldName>`` in [CoTTask.stateUpdates](CoTTask.md#attr-cottaskstateupdates).

**Flags**: IR

---
## Attr: Process.outputFields

### Description
Shorthand alternative to [Process.outputDS](#attr-processoutputds): a list of [DataSourceField](../reference_2.md#object-datasourcefield) definitions the engine compiles into a temporary validation DataSource on demand. The declared field names also govern which [Process.state](#attr-processstate) properties are picked into the Process's output value if [Process.setOutput](#method-processsetoutput) is never called.

See [processIO](../kb_topics/processIO.md#kb-topic-process-input-and-output-schema).

**Flags**: IR

---
## Attr: Process.errorTask

### Description
Process-level default for any task that fails without its own [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement) - the [Process](#class-process) analog of `failureElement`, one level up. When a task fails and has no `failureElement` of its own, its owning Process's [effective error task](#method-processgeteffectiveerrortask) is used instead, if one resolves. To designate an existing, hand-authored task on this same Process instead of a framework-provided default, use [Process.errorTaskRef](#attr-processerrortaskref) (a plain String ID) rather than this attribute.

Two kinds of value are meaningful:

*   A [ProcessElement](ProcessElement.md#class-processelement) instance, or a plain properties object naming a task type via `_constructor` (typically a [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask) or subclass). This is what propagates to sub-Processes (see below) - it is materialized as a real element of whichever Process actually needs it, so it works regardless of which Process in the ancestry declared it. Passing a literal, already-constructed instance means that same instance (and its [current process](ProcessElement.md#method-processelementsetcurrentprocess) link) is reused and retargeted by every Process that resolves to it; pass a plain properties object (the common case) to get an independent instance per Process instead.
*   `false`, to explicitly stop error-task propagation for this Process (and anything invoked as its sub-Process that does not declare its own `errorTask`/`errorTaskRef`) without affecting any other Process.

Unless one of the above (or [Process.errorTaskRef](#attr-processerrortaskref)) is set, this Process's effective error task is inherited from whichever Process invoked it as a [sub-process](SubProcessTask.md#class-subprocesstask) (see [Process.getEffectiveErrorTask](#method-processgeteffectiveerrortask)), and ultimately from [Process.getDefaultErrorTask](#classmethod-processgetdefaulterrortask) if [Process.defaultErrorHandlingEnabled](#classattr-processdefaulterrorhandlingenabled) is `true` and no Process in the ancestry configures anything at all.

**Flags**: IR

---
## Attr: Process.ruleScope

### Description
[Canvas.ID](Canvas.md#attr-canvasid) of the component that manages "rule context" for which this process participates. The rule context can be used in [taskInputExpression](../reference_2.md#type-taskinputexpression).

### See Also

- [Canvas.ruleScope](Canvas.md#attr-canvasrulescope)

**Flags**: IR

---
## Attr: Process.elements

### Description
Elements involved in this Process. You can also group elements into [Process.sequences](#attr-processsequences) to reduce the need to explicitly define IDs for elements and interlink them.

**Flags**: IR

---
## Attr: Process.wizard

### Description
If wizard is set then current workflow will be handled as wizard. Every userTask will hide associated form after user finished step.

**Flags**: IR

---
## Attr: Process.startElement

### Description
The ID of either a [sequence](#attr-processsequences) or an [element](#attr-processelements) which should be the starting point of the process. If not specified, the first sequence is chosen, or if there are no sequences, the first element. - log a warning and do nothing if there are neither sequences or elements - an example of how a Process would be defined
```
 isc.Process.create({
     startElement:"firstSequence", 
     sequences: [
         { 
            id:"firstSequence",
            elements : [
                isc.DSRequestTask.create({ .. }),
                isc.MultiDecisionTask.create({ .. })
            ]
         },
         {
            id:"errorFlow",
            elements : [ ... ]
            
         }
     ],
     elements: [
        // standalone process elements not part of sequences
        isc.DSRequestTask.create({ .. })
     ],
     state : {
         someField:"someValue"
     }
 })
 
```

**Flags**: IR

---
## Attr: Process.inputDS

### Description
Optional [DataSource](DataSource_1.md#class-datasource) that constrains the input record a caller may provide to this Process. May be a full DataSource definition, an existing instance, or the global ID of a registered DataSource. Nested DataSources are permitted.

When set, the input record is validated via [DataSource.validateData](DataSource_1.md#method-datasourcevalidatedata) before the Process starts.

See [processIO](../kb_topics/processIO.md#kb-topic-process-input-and-output-schema). If both `inputDS` and [Process.inputFields](#attr-processinputfields) are set, `inputDS` wins.

**Flags**: IR

---
## Attr: Process.traceContext

### Description
Context object to be passed to [Process.traceElement](#method-processtraceelement) during process execution.

**Flags**: IRWA

---
## Attr: Process.tasks

### Description
Convenience form of declaring a single, linear sequence of tasks for this process. Functionally equivalent to providing a one-element [sequences](#attr-processsequences) Array whose first (and only) member is this list.

If [Process.sequences](#attr-processsequences) is not provided, `process.tasks` becomes the sole sequence. If both are provided, `process.tasks` is inserted as the first sequence, followed by the declared `sequences`.

Each entry may be:

*   A plain Object, which will be auto-instantiated as a Task or a [StartProcessTask](StartProcessTask.md#class-startprocesstask) (wrapping a nested Process) using the heuristic documented on [Process.defaultTaskConstructor](#attr-processdefaulttaskconstructor) / [Process.defaultProcessConstructor](#attr-processdefaultprocessconstructor).
*   An already constructed [ProcessElement](ProcessElement.md#class-processelement) (or subclass) instance.

**Flags**: IR

---
## Attr: Process.defaultWaitFor

### Description
Condition to wait for before each task is executed. Task [waitFor](ProcessElement.md#attr-processelementwaitfor) can be specified for individual tasks to override this default.

For a value of "duration", the delay time is set by [Process.defaultWaitDuration](#attr-processdefaultwaitduration) and can be overridden by a task [waitDuration](ProcessElement.md#attr-processelementwaitduration).

Note that if `defaultWaitFor` is set to "systemDone" and a task overrides it with `waitFor` "locator", the default "systemDone" is not performed. To apply both, as might be desired, use task `waitFor` "locatorAndSystemDone".

A `defaultWaitFor` value of "locator" or "locatorAndSystemDone" is not valid.

**Flags**: IR

---
## Attr: Process.defaultTaskConstructor

### Description
Name of the default Task subclass to use when auto-constructing plain Objects found in collections that accept Tasks (for example [CoTProcess.tasks](#attr-processtasks), sequence members, etc).

This is consulted only when the element is a plain Object (not already constructed) and does not declare its own `_constructor`. If `defaultTaskConstructor` is unset for a given `Process`, the engine uses [ScriptTask](ScriptTask.md#class-scripttask).

#### Task vs nested subprocess heuristic
Nested Processes are often used to encapsulate a sub-workflow. When auto-constructing, the engine uses a heuristic to auto-detect the developer's intent to create a nested Process, as follows:

1.  If the element is already a constructed instance (Task or StartProcessTask), use it as-is.
2.  If the element declares `_constructor`, use that class directly.
3.  **If the element has a `process` property**:
    1.  Construct a [SubProcessTask](SubProcessTask.md#class-subprocesstask) for the element itself (unless the object declares its own `_constructor` to override this). SubProcessTask is a strict superset of [StartProcessTask](StartProcessTask.md#class-startprocesstask): with neither `stateUpdates` nor process-level I/O schemas declared it behaves identically to StartProcessTask; with them it additionally supports CoT-style state flow, [TaskInputExpression](../reference_2.md#type-taskinputexpression) `$output.`<fieldName>`` references, and infra-failure routing via `failureElement`.
    2.  If `process` is a plain Object (not already constructed), auto-instantiate it as a Process using [Process.defaultProcessConstructor](#attr-processdefaultprocessconstructor) and assign the instance to `task.process`.
    3.  If `process` is already a Process instance, assign it directly to `task.process`.
4.  Otherwise, construct it as a Task using [Process.defaultTaskConstructor](#attr-processdefaulttaskconstructor) if set, otherwise [Task](Task.md#class-task).

#### Examples
```
 // Plain objects default to CoTTask (AI module) unless specified otherwise.
 isc.Process.create({
   defaultTaskConstructor: "CoTTask",
   defaultProcessConstructor: "CoTProcess",
   tasks: [
     { ID:"decide",  title:"Decide Next" },   // -> CoTTask

     // Nested process via wrapper: becomes StartProcessTask; its .process is auto-created.
     { ID:"subflow",
       process: {
         ID:"p1",
         tasks:[ { ID:"leaf", title:"Leaf step" } ] // auto-instantiated as CoTProcess
       }
     },

     { _constructor:"MyTask", ID:"apply" }    // -> MyTask
   ]
 });
 
```

**Flags**: IR

---
## Attr: Process.strictPaths

### Description
If set to true, the process will not allow any intermediate state to be set via [Process.setStateVariable](#method-processsetstatevariable) that is not explicitly defined first.

**Flags**: IWR

---
## Attr: Process.mockMode

### Description
Enable mock mode on the workflow? By default, this setting does nothing but is available for individual tasks to trigger special action. For example, a task that would normally fail outside of its target environment can take an alternative action during testing.

mockMode can also be enabled or disabled for an individual task with [ProcessElement.mockMode](ProcessElement.md#attr-processelementmockmode).

**Flags**: IRW

---
## Attr: Process.errorTaskRef

### Description
ID of a task or [sequence](#attr-processsequences) declared directly on **this** Process to use as its [effective error task](#method-processgeteffectiveerrortask) - the [Process](#class-process) analog of [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement), one level up, for the common case of designating an existing, hand-authored task as the Process-wide fallback (rather than the framework-provided default - see [Process.errorTask](#attr-processerrortask) for that). Only meaningful on the Process that declares the referenced element - not inherited by sub-Processes, since a child Process has no visibility into a parent's own elements; use [Process.errorTask](#attr-processerrortask)'s properties-object form for anything that needs to propagate across Process boundaries.

Unlike [Process.errorTask](#attr-processerrortask), this is a plain String field (matching `failureElement`'s own declaration) and survives being exploded/collapsed through [process.getEditContext](#method-processgeteditcontext)/[Process.getPropertiesFromEditContext](#method-processgetpropertiesfromeditcontext) (as used by [WorkflowEditor](#class-workfloweditor)) correctly.

A task designated this way is an ordinary element like any other - nothing stops it from also being reachable via the Process's normal [ProcessElement.nextElement](ProcessElement.md#attr-processelementnextelement)/ branch flow, exactly as nothing stops a `failureElement` target from also being reachable normally. Set [Process.errorTaskExclusive](#attr-processerrortaskexclusive) to surface a (non-blocking) [WorkflowEditor](#class-workfloweditor) warning if that happens; the task itself always displays with its own description plus a distinguishing note in its title - see [workflowEditor.updateProcessNodeFromElement](#method-workfloweditorupdateprocessnodefromelement) for the underlying document and [Process.getTextSummary](#method-processgettextsummary) for the same note in a Workflow's bulleted summary.

**Flags**: IR

---
## Attr: Process.defaultWaitDuration

### Description
When [Process.defaultWaitFor](#attr-processdefaultwaitfor) or task [waitFor](ProcessElement.md#attr-processelementwaitfor) are set to "duration", how long should the wait be before starting the task? A task can override the default value with task [waitDuration](ProcessElement.md#attr-processelementwaitduration).

**Flags**: IR

---
## Attr: Process.errorTaskExclusive

### Description
When `true`, [WorkflowEditor](#class-workfloweditor) flags [Process.errorTaskRef](#attr-processerrortaskref)'s target (via [WorkflowEditor.validate](#method-workfloweditorvalidate)) if it is **also** reachable via the Process's normal [ProcessElement.nextElement](ProcessElement.md#attr-processelementnextelement)/branch flow - a likely authoring mistake, since a node designated as the Process-wide error handler is normally meant to be reached only via failure routing. This is a visual warning only; it does not block saving or executing the Process either way.

Default `false` matches `failureElement`'s own long-standing "no enforcement" contract for hand-authored Workflows - [WorkflowBuilderCoTProcess.createNewWorkflowProcess](#method-workflowbuildercotprocesscreatenewworkflowprocess) sets this `true` for Workflows it builds from scratch.

**Flags**: IR

---
## Attr: Process.containerId

### Description
Identifier of canvas where UI elements created by using [inline view](UserTask.md#attr-usertaskinlineview) property should be added using addMember.

**Flags**: IRW

---
## Attr: Process.autoStart

### Description
Cause the process to automatically call [Process.start](#method-processstart) as soon as it is created.

**Flags**: IR

---
## ClassMethod: Process.loadProcess

### Description
Loads an XML process definition stored in XML from the server.

This method requires server-side support included in SmartClient Pro Edition or better. If you are using SmartClient LGPL, Processes must be defined programmatically in JavaScript.

Process files are stored as .proc.xml files in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) format, in the directory indicated by the `project.processes` setting in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) (`_webroot_/processes` by default). To load a process saved in a file _processId_.proc.xml, pass just _processId_ to this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| processId | [Identifier](../reference_2.md#type-identifier)|[Array of Identifier](#type-array-of-identifier) | false | — | process ID or IDs to load |
| callback | [ProcessCallback](#type-processcallback) | false | — | called when the process is loaded with argument "process", the first process. Other processes can be looked up via [Process.getProcess](#classmethod-processgetprocess). |

---
## ClassMethod: Process.getProcess

### Description
Get a Process instance by its ID.

Each process instance created that has an [ID](ProcessElement.md#attr-processelementid) is cached for later lookup by that ID. If two processes have the same ID the last one is cached, overwriting the first. Note that the process instances are not affected - only the cache reference.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| processId | [Identifier](../reference_2.md#type-identifier) | false | — | process ID to retrieve |

### Returns

`[Process](#type-process)` — the process, or null if not found

### See Also

- [Process.loadProcess](#classmethod-processloadprocess)

---
## ClassMethod: Process.classifyError

### Description
Classifies a task failure as ["expected"](../reference_2.md#type-errorcategory) or "unexpected", for [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask) to decide whether to show the standard centralized error dialog. Default classification mirrors [RPCManager](../kb_topics/errorHandling.md#kb-topic-error-handling-overview)'s own documented validation-vs-other-errors split: a [ErrorContext.failure](../reference.md#attr-errorcontextfailure) whose `code` is `"inputValidation"`, `"outputValidation"`, or `"cancelled"` is "expected", as is a [ErrorContext.response](../reference.md#attr-errorcontextresponse) whose status is [RPCResponse.STATUS_VALIDATION_ERROR](RPCResponse.md#classattr-rpcresponsestatus_validation_error); everything else is "unexpected".

Override to widen or change this split for your application - for example, in a network-diagnostics tool where users routinely type unreachable hostnames, classify [RPCResponse.STATUS_UNKNOWN_HOST_ERROR](RPCResponse.md#classattr-rpcresponsestatus_unknown_host_error)/ [RPCResponse.STATUS_TRANSPORT_ERROR](RPCResponse.md#classattr-rpcresponsestatus_transport_error) as "expected" too. The full [ErrorContext](#type-errorcontext) is passed (not just the response status) so an override can consult anything relevant to a better decision - the failed [ErrorContext.task](../reference.md#attr-errorcontexttask), the owning [ErrorContext.process](../reference.md#attr-errorcontextprocess) and its [Process.state](#attr-processstate), and so on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| context | [ErrorContext](#type-errorcontext) | false | — | every signal available about the failure |

### Returns

`[ErrorCategory](../reference_2.md#type-errorcategory)` — "expected" or "unexpected"

---
## ClassMethod: Process.getDefaultErrorTask

### Description
Returns the task configuration used as ${isc.DocUtils.linkForRef('attr:Process.errorTask','every Process\\'s default\\n error task')} when [Process.defaultErrorHandlingEnabled](#classattr-processdefaulterrorhandlingenabled) is `true` and neither the Process nor any ancestor Process declares its own `errorTask`. Default implementation returns a plain [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask) configuration; override to change the framework-wide default (for example, to a subclass that also logs to an audit DataSource) without editing every Process.

### Returns

`[ProcessElement Properties](#type-processelement-properties)` — properties for a new [UnexpectedErrorTask](UnexpectedErrorTask.md#class-unexpectederrortask)

---
## Method: Process.setTaskOutput

### Description
Sets the task output of `task` in the [process state](../reference.md#type-state) so it can be used by later tasks with [Process.getLastTaskOutput](#method-processgetlasttaskoutput) or more commonly with a [TaskInputExpression](../reference_2.md#type-taskinputexpression) property.

If the task sets `bindOutput` the output value is also written into that [process state](#attr-processstate) variable.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [ProcessElement](#type-processelement) | false | — | the workflow task setting the output (i.e. this) |
| value | [Any](#type-any) | false | — | the output value for task |

---
## Method: Process.getProcessState

### Description
Returns the complete process state for persistence. This includes not just process.state, but execution position and transient data needed to resume the workflow.

### Returns

`[Object](../reference.md#type-object)` — Complete state object with: - state: process.state variables - execution: current execution position - transientData: task outputs that feed into subsequent tasks

---
## Method: Process.restoreFromState

### Description
Restores process state from a previously saved complete state and optionally resumes execution.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| completeState | [Object](../reference.md#type-object) | false | — | State object from getProcessState() |
| resume | [Boolean](#type-boolean) | true | — | If true, immediately resume execution after restore |

---
## Method: Process.reset

### Description
Reset process to its initial state, so process can be started again.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | true | — | new state of the process |

---
## Method: Process.suspend

### Description
Suspends process execution at the current point. The process state can be retrieved via getProcessState() for persistence.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | false | — | Reason for suspension (e.g., "HumanTask", "Timer") |
| taskId | [String](#type-string) | false | — | ID of the task where process is suspended |

---
## Method: Process.getComponentReferences

### Description
Returns a list of unique global IDs that are referenced by this process.

List is assembled by calling [ProcessElement.getComponentReferences](ProcessElement.md#method-processelementgetcomponentreferences) for each task in the workflow and filtering the list to the unique component IDs.

### Returns

`[Array of String](#type-array-of-string)` — array of component IDs that are referenced by this process

---
## Method: Process.setOutput

### Description
Explicitly set the final output this Process will deliver on successful completion, overriding the default behavior of picking output fields out of [Process.state](#attr-processstate). Callable from anywhere during execution; the most recent value wins.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| output | [Any](#type-any) | false | — | the output value to deliver |

---
## Method: Process.getEffectiveErrorTask

### Description
Resolves this Process's effective error task: [Process.errorTaskRef](#attr-processerrortaskref) if set (an explicit reference to an existing task declared on this Process); else [Process.errorTask](#attr-processerrortask) if set (including an explicit `false`, which resolves to `null`); else the invoking parent Process's effective error task (if this Process was started as a [sub-process](SubProcessTask.md#class-subprocesstask)); else [Process.getDefaultErrorTask](#classmethod-processgetdefaulterrortask) when [Process.defaultErrorHandlingEnabled](#classattr-processdefaulterrorhandlingenabled) is `true`.

`errorTaskRef` is returned directly (it already names an element declared here). A resolved [Process.errorTask](#attr-processerrortask) value (a ProcessElement instance, or a properties object identifying one) is materialized as a real element of this Process - registered under a stable, well-known ID so a String suitable for [Process.setNextElement](#method-processsetnextelement) is always what's returned.

### Returns

`[String](#type-string)` — ID of the effective error task, or null if none resolves

---
## Method: Process.getErrorTaskExclusivityViolation

### Description
Checks whether [Process.errorTaskRef](#attr-processerrortaskref)'s target is **also** reachable via this Process's normal [ProcessElement.nextElement](ProcessElement.md#attr-processelementnextelement)/branch flow, regardless of whether [Process.errorTaskExclusive](#attr-processerrortaskexclusive) is set - [WorkflowEditor](#class-workfloweditor) calls this itself only when that flag is `true`, but the check is exposed unconditionally so other callers (e.g. a custom pre-save check) can use it too.

### Returns

`[String](#type-string)` — errorTaskRef's value, if it is also normally reachable; else null

---
## Method: Process.applyStateUpdates

### Description
Apply the state updates specified by [Process.setStateVariable](#method-processsetstatevariable) to the process state.

`stateUpdates` is a mapping from a [setterPath](../reference_2.md#type-setterpath) to a ${TaskInputExpression} or other value.

`stateUpdates` can declare nested structures, and `TaskInputExpressions` are allowed anywhere in the nested declaration.

```
       {
               "currentDS.fields[]" : "$output"
               "lastCreatedField" : {
                     "fromTask" : "Add Field",
                     "fieldName" : "$output.name"
               }
       }
 
```
In this example, the output is appended to the "currentDS.fields" array in [Process.state](#attr-processstate) and an object called "lastCreatedField" is created in `process.state.lastCreatedField`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stateUpdates | [Object](../reference.md#type-object) | false | — | state updates to apply |
| inputRecord | [Object](../reference.md#type-object) | true | — | record to use as the source for any $input [TaskInputExpression](../reference_2.md#type-taskinputexpression) properties. |
| strict | [Boolean](#type-boolean) | true | — | if true, the paths must exist in the state to be set. Otherwise, the paths will be created if not existing. Defaults to `process.strictPaths` when null. |

---
## Method: Process.fail

### Description
Programmatically signal that this Process has hit an infrastructure failure and should terminate through its [Process.failed](#method-processfailed) channel rather than completing normally. Recoverable errors that are part of the Process's designed output schema should NOT use this path; model them as fields in [Process.outputDS](#attr-processoutputds).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| code | [String](#type-string) | false | — | short identifier, e.g. `"aiUnavailable"`. See [ProcessFailure](#type-processfailure). |
| message | [String](#type-string) | true | — | human-readable description |
| cause | [Any](#type-any) | true | — | optional underlying exception or nested failure |

---
## Method: Process.getElement

### Description
Retrieve a [ProcessElement](ProcessElement.md#class-processelement) by its ID

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | id of the process element |

### Returns

`[ProcessElement](#type-processelement)` — the indicated process element, or null if no such element exists

---
## Method: Process.traceElement

### Description
StringMethod called during process execution before each task element is processed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [Task](#type-task) | false | — | the [Task](Task.md#class-task) being executed |
| context | [Object](../reference.md#type-object) | false | — | the [Process.traceContext](#attr-processtracecontext), if set |

---
## Method: Process.getStateVariable

### Description
Returns a variable value from the [process state](#attr-processstate). Values can be written into the process state by [Process.setStateVariable](#method-processsetstatevariable), setting [ProcessElement.bindOutput](ProcessElement.md#attr-processelementbindoutput), or various task output settings (See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stateVariablePath | [String](#type-string) | false | — | path to variable in process state to set. segments are separated by a decimal point (.) |

### Returns

`[Any](#type-any)` — the value found at the path

---
## Method: Process.setStateVariable

### Description
Sets a [process state](#attr-processstate) variable for later reference with [Process.getStateVariable](#method-processgetstatevariable) or more commonly with a [TaskInputExpression](../reference_2.md#type-taskinputexpression) property.

The path, which is one or more valid identifiers separated by periods, is used to identify the variable. By appending an empty pair of brackets (\[\]) the value will be placed into an existing or new array at the specified path.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stateVariablePath | [SetterPath](../reference_2.md#type-setterpath) | false | — | path to the variable in the process state to set. |
| value | [Any](#type-any) | false | — | the value to save |
| strict | [Boolean](#type-boolean) | true | — | if true, the path must exist in the state to be set. Otherwise, the path will be created if it does not exist. Defaults to `process.strictPaths` when null. |

---
## Method: Process.setNextElement

### Description
Sets the task ID of the next task to execute after the current task finishes. If the task is not found or `null` is passed as the nextElement, the current process will be terminated instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nextElement | [String](#type-string) | true | — | ID of the next task execute or null to terminate the process |

---
## Method: Process.failed

### Description
StringMethod called when a process terminates via an infrastructure failure - for example AI engine unavailable, schema-validation mismatch on input or output, uncaught JS exception, cancellation, or an ancestor-cycle deadlock when invoking a sub-Process. Recoverable errors that are part of the Process's designed output do NOT come through here; they live inside the successful [finished](#method-processfinished) result.

See [ProcessFailure](#type-processfailure) for the shape of the argument.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| failure | [ProcessFailure](#type-processfailure) | false | — | the failure record |

---
## Method: Process.getLastTaskOutput

### Description
Returns the task output of the last task executed. More commonly a [TaskInputExpression](../reference_2.md#type-taskinputexpression) property is used (see [ProcessElement.getDynamicValue](ProcessElement.md#method-processelementgetdynamicvalue)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskType | [String](#type-string) | true | — | the optional task type to lookup in last task output |

### Returns

`[Any](#type-any)` — the last task output or null if none is found

---
## Method: Process.getSuspendInfo

### Description
Returns information about why and where the process is suspended.

### Returns

`[Object](../reference.md#type-object)` — Object with reason and taskId, or null if not suspended

---
## Method: Process.getProcessDescription

### Description
Returns the process description as HTML.

### Returns

`[String](#type-string)` — the process description as HTML

---
## Method: Process.afterTaskCommit

### Description
Notification hook invoked after a Task's outputs have been committed to state and history recorded, but before routing to the next element. Use for ancillary effects such as logging, metrics, or scheduling background work. This hook cannot veto the commit; to inject validation or replace outputs, use [Process.beforeTaskCommit](#method-processbeforetaskcommit).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [Task](#type-task) | false | — | The Task that just committed. |
| outputs | [Object](../reference.md#type-object) | false | — | The committed outputs (if any). |

---
## Method: Process.getOutput

### Description
Returns the Process's output, computed in this priority order:

1.  The value passed to [Process.setOutput](#method-processsetoutput) if any.
2.  If [Process.outputDS](#attr-processoutputds)/[Process.outputFields](#attr-processoutputfields) are declared: a shallow pick of those field names from [Process.state](#attr-processstate).
3.  Otherwise: [Process.state](#attr-processstate) itself (back-compat).

### Returns

`[Any](#type-any)` — the computed output

---
## Method: Process.start

### Description
Starts this task by executing the [Process.startElement](#attr-processstartelement). Also used by asynchronous tasks to restart the workflow.

---
## Method: Process.finished

### Description
StringMethod called when a process completes, meaning the process executes a ProcessElement with no next element.

Handlers declared with a single `(state)` signature remain supported; the second argument is ignored harmlessly for such handlers. Handlers that want the schema-validated result use the two-argument form.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | false | — | the final process state |
| output | [Any](#type-any) | false | — | the Process's validated output, as computed by [Process.getOutput](#method-processgetoutput). When no output schema is declared, this is the same object as `state`. |

---
## Method: Process.runTask

### Description
Execute a single task in isolation for testing. The process must not already be running. This method invokes the specified task once without advancing the workflow.

Typically used for automated tests of complex tasks, including those involving AI.

Providing `priorTaskOutputs` means that [TaskInputExpressions](../reference_2.md#type-taskinputexpression) and other forms of [Task.inputs](Task.md#attr-taskinputs) declarative inputs will draw from the provided data. For example, $outputs.propertyName used as an expression would refer to the value under `propertyName` in the provided priorTaskOutputs object.

If `state` is supplied, it is used as the temporary process state for this call (the original state is preserved). If `ruleScope` is supplied, it replaces the normal [ruleScope determination](#attr-processrulescope) for this invocation only.

When the task completes, `callback` (a [Callbacks.RunTaskCallback](Callbacks.md#method-callbacksruntaskcallback)) is invoked with the task, process, and any outputs the task produced (for example, a CoTTask’s `$outputs`).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskID | [String](#type-string) | false | — | ID of the task to execute. |
| callback | [RunTaskCallback](#type-runtaskcallback) | false | — | Completion callback. |
| priorTaskOutputs | [Object](../reference.md#type-object) | false | — | Optional object to simulate outputs from a prior task (see behavior above). |
| state | [Object](../reference.md#type-object) | false | — | Optional state fixture to use for this call. |
| ruleContext | [Object](../reference.md#type-object) | false | — | Optional override ruleContext for expression evaluation. |

---
## Method: Process.passThruTaskOutput

### Description
Takes the [last task output](#method-processgetlasttaskoutput) and sets it as the [task output](#method-processsettaskoutput) for the `task`.

This method is not just a shortcut to set output of a pass-thru task, but it also records the correct schema of the passed-thru output so it can be quickly looked up.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [ProcessElement](#type-processelement) | false | — | the workflow task setting the output (i.e. this) |

---
## Method: Process.isSuspended

### Description
Returns true if the process is currently suspended.

### Returns

`[Boolean](#type-boolean)` — true if suspended

---
## Method: Process.resume

### Description
Resumes a suspended process. If the process was suspended at a HumanTask, the taskOutput should contain the result of the human task completion.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskOutput | [Object](../reference.md#type-object) | true | — | Output from the completed async task |

---
## Method: Process.getTextSummary

### Description
Returns a plain bulleted-text summary of this Process's current tasks - one bullet per task, using [ProcessElement.getInstanceTitle](ProcessElement.md#method-processelementgetinstancetitle) and [ProcessElement.getInstanceDescription](ProcessElement.md#method-processelementgetinstancedescription) - suitable for a non-technical review of what a Process does without opening [WorkflowEditor](#class-workfloweditor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| markUnreferencedTasks | [Boolean](#type-boolean) | true | — | include tasks not reachable from the normal flow, as a trailing series - see [getProcessTree](#method-getprocesstree) |
| unnamedSequencePrefix | [String](#type-string) | true | — | prefix used for auto-generated sequence IDs - see [getProcessTree](#method-getprocesstree) |

### Returns

`[String](#type-string)` — bulleted-text summary, one line per task

---
## Method: Process.beforeTaskCommit

### Description
Override point invoked after a Task completes successfully, but before any of the Task's outputs are committed to [Process.state](#attr-processstate) and before next-task routing proceeds. Use this to:

*   Inject global validation and force a retry by returning errors.
*   Augment or replace the Task's outputs prior to commit.
*   Apply additional declarative updates to [state](#attr-processstate).

Return a [TaskResultModifications](../reference_2.md#object-taskresultmodifications) object to influence commit behavior. If you return nothing, the engine proceeds normally.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [ProcessElement](#type-processelement) | false | — | The Task or sub-Process that just completed. |
| outputs | [Object](../reference.md#type-object) | false | — | The Task's outputs |

### Returns

`[TaskResultModifications](#type-taskresultmodifications)` — Optional result to modify commit behavior.

---
## Method: Process.setState

### Description
Set process state for current process

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | false | — | the new process state |

---
