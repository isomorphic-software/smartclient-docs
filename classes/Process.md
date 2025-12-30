# Process Documentation

[← Back to API Index](../reference.md)

---

## Class: Process

*Inherits from:* [Task](Task.md#class-task)

### Description
A instance of Process represents a stateful process executing a series of Tasks, which may be:

*   user interactions
*   calls to DataSources (hence: any database or web service)
*   arbitrary code
*   other Processes

A Process is _stateful_ in the sense that it maintains [state](#attr-processstate) across the different tasks that are executed. This allows you to maintain context as you walk a user through a multi-step business process in your application, which may involve multiple operations on multiple entities. Each Task that executes can use the Process state as inputs, and can output a result which is stored in the Process state - see [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

A Process can have multiple branches, choosing the next Task to execute based on [Criteria](../reference.md#type-criteria) - see [XORGateway](XORGateway.md#class-xorgateway) and [DecisionGateway](DecisionGateway.md#class-decisiongateway).

Because a Process may return to a previous Task in various situations, the data model of a Process is strictly speaking a _graph_ (a set of nodes connected by arbitary interlinks). However, most processes have sequences of several tasks in a row, and the definition format allows these to be represented as simple Arrays called "sequences", specified via [Process.sequences](#attr-processsequences). This reduces the need to manually specify IDs and interlinks for Tasks that simply proceed to the next task in a sequence.

Processes follow all the standard rules for encoding as [componentXML](../kb_topics/componentXML.md#kb-topic-component-xml), however, note that the `<Process>` tag allows any kind of [ProcessElement](ProcessElement.md#class-processelement) (tasks, gateways and sequences) to appear as a direct subelement of the `<Process>` tag without the need for an intervening `<elements>` or `<sequences>` tag. The example below demonstrates this shorthand format.

```
 <Process ID="processId">
     <ServiceTask ID="serviceTaskId" nextElement="sequenceId" ..>
         <inputFieldList>
             <value>order.countryName</value>
         </inputFieldList>
         <outputFieldList>
             <value>order.countryName</value>
             <value>order.continent</value>
         <outputFieldList>
     </ServiceTask>
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
_**NOTE:** you must load the Workflow module [Optional Modules](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) before you can use `Process`._

---
## Attr: Process.state

### Description
Current state of a process. As with Records in general, any field of a Record may contain a nested Record or Array of Records, so the process state is essentially a hierarchical data structure.

#### Transient state
In addition to the explicit process state there is a "transient state." The transient state represents the complete output of each of the last tasks of each type within the current process execution. This allows easy reference to the previous task output with [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions).

**Flags**: IRW

---
## Attr: Process.sequences

### Description
Sequences of ProcessElements. By defining a sequences of elements you can make the [ProcessElement.nextElement](ProcessElement.md#attr-processelementnextelement) implicit.

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
## Attr: Process.ruleScope

### Description
[Canvas.ID](Canvas.md#attr-canvasid) of the component that manages "rule context" for which this process participates. The rule context can be used in [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions).

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
                isc.ServiceTask.create({ .. }),
                isc.DecisionGateway.create({ .. })
            ]
         },
         {
            id:"errorFlow",
            elements : [ ... ]
            
         }
     ],
     elements: [
        // standalone process elements not part of sequences
        isc.ServiceTask.create({ .. })
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
## ClassMethod: Process.getProcess

### Description
Get a Process instance by it's ID. See [Process.loadProcess](#classmethod-processloadprocess).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| processId | [Identifier](../reference.md#type-identifier) | false | — | process IDs to retrieve |

### Returns

`[Process](#type-process)` — the process, or null if not loaded

---
## ClassMethod: Process.loadProcess

### Description
Loads an XML process definition stored in XML from the server.

This method requires server-side support included in SmartClient Pro Edition or better.

Process files are stored as .proc.xml files in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) format, in the directory indicated by the `project.processes` setting in [server.properties](../reference.md#kb-topic-serverproperties-file) (`_webroot_/processes` by default). To load a process saved in a file _processId_.proc.xml, pass just _processId_ to this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| processId | [Identifier](../reference.md#type-identifier)|[Array of Identifier](#type-array-of-identifier) | false | — | process IDs to load |
| callback | [ProcessCallback](#type-processcallback) | false | — | called when the process is loaded with argument "process", the first process. Other processes can be looked up via [Process.getProcess](#classmethod-processgetprocess). |

---
## Method: Process.reset

### Description
Reset process to it's initial state, so process can be started again.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | false | — | new state of the process |

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
## Method: Process.getElement

### Description
Retrieve a [ProcessElement](ProcessElement.md#class-processelement) by it's ID

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | id of the process element |

### Returns

`[ProcessElement](#type-processelement)` — the indicated process element, or null if no such element exists

---
## Method: Process.setState

### Description
Set process state for current process

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Record](#type-record) | false | — | the new process state |

---
## Method: Process.traceElement

### Description
StringMethod called during process execution before each task element is processed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [Task](#type-task) | false | — | the [Task](Task.md#class-task) being executed |
| context | [Object](../reference_2.md#type-object) | false | — | the [Process.traceContext](#attr-processtracecontext), if set |

---
