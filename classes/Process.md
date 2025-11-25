# Process Documentation

[← Back to API Index](../main.md)

---

## Class: Process

### Description
A instance of Process represents a stateful process executing a series of Tasks, which may be:

*   user interactions
*   calls to DataSources (hence: any database or web service)
*   arbitrary code
*   other Processes

A Process is _stateful_ in the sense that it maintains [state](#attr-processstate) across the different tasks that are executed. This allows you to maintain context as you walk a user through a multi-step business process in your application, which may involve multiple operations on multiple entities. Each Task that executes can use the Process state as inputs, and can output a result which is stored in the Process state - see [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

A Process can have multiple branches, choosing the next Task to execute based on [Criteria](../main_2.md#type-criteria) - see [DecisionTask](DecisionTask.md#class-decisiontask) and [MultiDecisionTask](MultiDecisionTask.md#class-multidecisiontask).

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
## ClassAttr: Process.decisionPlaceholderSelection

### Description
Value of `failureElement` in various [tasks](ProcessElement.md#class-processelement) to indicate a placeholder is being used. Also applies to [DecisionBranch.targetTask](DecisionBranch.md#attr-decisionbranchtargettask) and [MultiDecisionTask.defaultElement](MultiDecisionTask.md#attr-multidecisiontaskdefaultelement).

**Flags**: IR

---
## Attr: Process.state

### Description
Current state of a process. As with Records in general, any field of a Record may contain a nested Record or Array of Records, so the process state is essentially a hierarchical data structure.

#### Transient state
In addition to the explicit process state there is a "transient state." The transient state represents the complete output of each of the last tasks of each type within the current process execution. This allows easy reference to the previous task output with [taskInputExpressions](../main_2.md#type-taskinputexpression).

**Flags**: IRW

---
## Attr: Process.defaultProcessConstructor

### Description
Name of the default Process subclass to use when auto-constructing plain Objects that are detected as Processes (see heuristic on [Process.defaultTaskConstructor](#attr-processdefaulttaskconstructor))

**Flags**: IR

---
## Attr: Process.sequences

### Description
Sequences of ProcessElements. By defining a sequences of elements you can make the [ProcessElement.nextElement](ProcessElement.md#attr-processelementnextelement) implicit.

For a simple sequence of tasks, consider using [Process.tasks](#attr-processtasks) instead.

You do not have to explicitly create a [ProcessSequence](../main.md#class-processsequence), you can instead use the shorthand:

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
## Attr: Process.ruleScope

### Description
[Canvas.ID](Canvas.md#attr-canvasid) of the component that manages "rule context" for which this process participates. The rule context can be used in [taskInputExpression](../main_2.md#type-taskinputexpression).

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
    1.  Construct a [StartProcessTask](StartProcessTask.md#class-startprocesstask) for the element itself (unless the object declares its own `_constructor` to override this).
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
## Attr: Process.defaultWaitDuration

### Description
When [Process.defaultWaitFor](#attr-processdefaultwaitfor) or task [waitFor](ProcessElement.md#attr-processelementwaitfor) are set to "duration", how long should the wait be before starting the task? A task can override the default value with task [waitDuration](ProcessElement.md#attr-processelementwaitduration).

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
| processId | [Identifier](../main.md#type-identifier)|[Array of Identifier](#type-array-of-identifier) | false | — | process ID or IDs to load |
| callback | [ProcessCallback](#type-processcallback) | false | — | called when the process is loaded with argument "process", the first process. Other processes can be looked up via [Process.getProcess](#classmethod-processgetprocess). |

---
## ClassMethod: Process.getProcess

### Description
Get a Process instance by its ID.

Each process instance created that has an [ID](ProcessElement.md#attr-processelementid) is cached for later lookup by that ID. If two processes have the same ID the last one is cached, overwriting the first. Note that the process instances are not affected - only the cache reference.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| processId | [Identifier](../main.md#type-identifier) | false | — | process ID to retrieve |

### Returns

`[Process](#type-process)` — the process, or null if not found

### See Also

- [Process.loadProcess](#classmethod-processloadprocess)

---
## Method: Process.setTaskOutput

### Description
Sets the task output of `task` in the [process state](../main.md#type-state) so it can be used by later tasks with [Process.getLastTaskOutput](#method-processgetlasttaskoutput) or more commonly with a [TaskInputExpression](../main_2.md#type-taskinputexpression) property.

If the task sets `bindOutput` the output value is also written into that [process state](#attr-processstate) variable.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [ProcessElement](#type-processelement) | false | — | the workflow task setting the output (i.e. this) |
| value | [Any](#type-any) | false | — | the output value for task |

---
## Method: Process.reset

### Description
Reset process to its initial state, so process can be started again.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | true | — | new state of the process |

---
## Method: Process.getComponentReferences

### Description
Returns a list of unique global IDs that are referenced by this process.

List is assembled by calling [ProcessElement.getComponentReferences](ProcessElement.md#method-processelementgetcomponentreferences) for each task in the workflow and filtering the list to the unique component IDs.

### Returns

`[Array of String](#type-array-of-string)` — array of component IDs that are referenced by this process

---
## Method: Process.applyStateUpdates

### Description
Apply the state updates specified by [Process.setStateVariable](#method-processsetstatevariable) to the process state.

`stateUpdates` is a mapping from a [setterPath](../main_2.md#type-setterpath) to a ${TaskInputExpression} or other value.

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
| stateUpdates | [Object](../main.md#type-object) | false | — | state updates to apply |
| inputRecord | [Object](../main.md#type-object) | true | — | record to use as the source for any $input [TaskInputExpression](../main_2.md#type-taskinputexpression) properties. |
| strict | [Boolean](#type-boolean) | true | — | if true, the paths must exist in the state to be set. Otherwise, the paths will be created if not existing. Defaults to `process.strictPaths` when null. |

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
| context | [Object](../main.md#type-object) | false | — | the [Process.traceContext](#attr-processtracecontext), if set |

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
Sets a [process state](#attr-processstate) variable for later reference with [Process.getStateVariable](#method-processgetstatevariable) or more commonly with a [TaskInputExpression](../main_2.md#type-taskinputexpression) property.

The path, which is one or more valid identifiers separated by periods, is used to identify the variable. By appending an empty pair of brackets (\[\]) the value will be placed into an existing or new array at the specified path.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stateVariablePath | [SetterPath](../main_2.md#type-setterpath) | false | — | path to the variable in the process state to set. |
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
## Method: Process.getLastTaskOutput

### Description
Returns the task output of the last task executed. More commonly a [TaskInputExpression](../main_2.md#type-taskinputexpression) property is used (see [ProcessElement.getDynamicValue](ProcessElement.md#method-processelementgetdynamicvalue)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskType | [String](#type-string) | true | — | the optional task type to lookup in last task output |

### Returns

`[Any](#type-any)` — the last task output or null if none is found

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
| outputs | [Object](../main.md#type-object) | false | — | The committed outputs (if any). |

---
## Method: Process.start

### Description
Starts this task by executing the [Process.startElement](#attr-processstartelement). Also used by asynchronous tasks to restart the workflow.

---
## Method: Process.finished

### Description
StringMethod called when a process completes, meaning the process executes a ProcessElement with no next element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | false | — | the final process state |

---
## Method: Process.runTask

### Description
Execute a single task in isolation for testing. The process must not already be running. This method invokes the specified task once without advancing the workflow.

Typically used for automated tests of complex tasks, including those involving AI.

Providing `priorTaskOutputs` means that [TaskInputExpressions](../main_2.md#type-taskinputexpression) and other forms of [Task.inputs](Task.md#attr-taskinputs) declarative inputs will draw from the provided data. For example, $outputs.propertyName used as an expression would refer to the value under `propertyName` in the provided priorTaskOutputs object.

If `state` is supplied, it is used as the temporary process state for this call (the original state is preserved). If `ruleScope` is supplied, it replaces the normal [ruleScope determination](#attr-processrulescope) for this invocation only.

When the task completes, `callback` (a [Callbacks.RunTaskCallback](Callbacks.md#method-callbacksruntaskcallback)) is invoked with the task, process, and any outputs the task produced (for example, a CoTTask’s `$outputs`).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskID | [String](#type-string) | false | — | ID of the task to execute. |
| callback | [RunTaskCallback](#type-runtaskcallback) | false | — | Completion callback. |
| priorTaskOutputs | [Object](../main.md#type-object) | false | — | Optional object to simulate outputs from a prior task (see behavior above). |
| state | [Object](../main.md#type-object) | false | — | Optional state fixture to use for this call. |
| ruleContext | [Object](../main.md#type-object) | false | — | Optional override ruleContext for expression evaluation. |

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
## Method: Process.beforeTaskCommit

### Description
Override point invoked after a Task completes successfully, but before any of the Task's outputs are committed to [Process.state](#attr-processstate) and before next-task routing proceeds. Use this to:

*   Inject global validation and force a retry by returning errors.
*   Augment or replace the Task's outputs prior to commit.
*   Apply additional declarative updates to [state](#attr-processstate).

Return a [TaskResultModifications](../main.md#object-taskresultmodifications) object to influence commit behavior. If you return nothing, the engine proceeds normally.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [ProcessElement](#type-processelement) | false | — | The Task or sub-Process that just completed. |
| outputs | [Object](../main.md#type-object) | false | — | The Task's outputs |

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
