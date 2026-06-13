# SubProcessTask Documentation

[← Back to API Index](../reference.md)

---

## Class: SubProcessTask

*Inherits from:* [StartProcessTask](StartProcessTask.md#class-startprocesstask)

### Description
Task that invokes another [Process](Process.md#class-process) as a sub-workflow using a declarative state-flow spec identical in feel to how regular tasks consume and produce state. A SubProcessTask is the right choice for [chain-of-thought processes](CoTProcess.md#class-cotprocess) and for any Process that declares [Process.inputDS](Process.md#attr-processinputds), [Process.outputDS](Process.md#attr-processoutputds), or CoT-style [stateUpdates](CoTTask.md#attr-cottaskstateupdates).

#### Relationship to StartProcessTask
SubProcessTask is a strict superset of [StartProcessTask](StartProcessTask.md#class-startprocesstask). With neither `stateUpdates` nor any process-level I/O schemas declared it behaves identically to StartProcessTask. With them it additionally:

1.  Validates the inputRecord against the child's [Process.inputDS](Process.md#attr-processinputds), routing mismatches to [failureElement](#processelementfailureelement) as infra failure `code:"inputValidation"`.
2.  Merges the inputRecord into the child's state (rather than replacing it), so CoTProcess's seeded `state.history` and other init-time state survive.
3.  Honors the [stateUpdates](CoTTask.md#attr-cottaskstateupdates) mapping using the child's validated [output](Process.md#method-processgetoutput) as the source for `$output.`<fieldName>`` expressions.
4.  Routes any infra failure raised by the child via [Process.failed](Process.md#method-processfailed) to this task's `failureElement`, or escalates via [Process.fail](Process.md#method-processfail) when `failureElement` is not declared.
5.  Detects direct or indirect self-invocation (ancestor cycle) and fails fast as `code:"reentry"` rather than deadlocking on the shared-instance reuse latch.

#### Declaration
SubProcessTask is built implicitly when a plain Object with a `process` property appears in a [Process.tasks](Process.md#attr-processtasks) / [ProcessSequence.elements](../reference.md#attr-processsequenceelements) array (see the auto-construction heuristic on [Process.defaultTaskConstructor](Process.md#attr-processdefaulttaskconstructor)). A typical inline declaration:
```
 tasks: [
     { ID: "analyze",
       process: "reportAnalyzer",                   // Process ID or instance
       inputs:  { text: "$state.rawReport" },       // parent.state -> child inputRecord
       stateUpdates: {                              // child.output -> parent.state
           severity:     "$output.severity",
           "tags[]":     "$output.categories"
       },
       failureElement: "handleInfraFailure"         // optional
     }
 ]
 
```
See the [Process I/O Schema](../kb_topics/processIO.md#kb-topic-process-input-and-output-schema) overview for the schema side and [TaskInputExpression](../reference_2.md#type-taskinputexpression) for the full list of input-expression prefixes.

### Groups

- serverProcess

---
## Attr: SubProcessTask.stateUpdates

### Description
Same [SetterPath](../reference_2.md#type-setterpath)-to-[TaskInputExpression](../reference_2.md#type-taskinputexpression) mapping as [CoTTask.stateUpdates](CoTTask.md#attr-cottaskstateupdates). Applied after the child Process completes successfully, with the child's validated output serving as the record referenced by `$output.`<fieldName>`` expressions (and by `$outputs`, which is treated as an alias here).

SetterPath operators `[]` (array append), `{}` (shallow merge, overwrite) and `{?}` (shallow merge, preserve existing) are honored just as in CoTTask.

**Flags**: IRW

---
## Attr: SubProcessTask.failureElement

### Description
ID of the task to branch to when the child raises an infrastructure failure (anything delivered via [Process.failed](Process.md#method-processfailed)). The sentinel `"next"` continues the linear sequence instead of branching. When unset the infra failure escalates to the parent Process via [Process.fail](Process.md#method-processfail).

Recoverable errors that are part of the child's successful output (carried through [Process.outputDS](Process.md#attr-processoutputds) fields) do NOT route here; the parent handles them via `stateUpdates` and any downstream decision tasks.

**Flags**: IRW

---
## Attr: SubProcessTask.inputs

### Description
Inherited from [Task.inputs](Task.md#attr-taskinputs). Describes what parent-process values are handed to the child as its input record. The resolved inputRecord is validated against the child's [Process.inputDS](Process.md#attr-processinputds) / [Process.inputFields](Process.md#attr-processinputfields) (if declared) and then merged into the child's initial state.

**Flags**: IRW

---
## Attr: SubProcessTask.process

### Description
Inherited from [StartProcessTask.process](StartProcessTask.md#attr-startprocesstaskprocess). The Process to run as a sub-workflow; may be an instance or a String ID resolvable via [screen](Canvas.md#class-canvas).getWorkflowById or [Process.getProcess](Process.md#classmethod-processgetprocess).

**Flags**: IRW

---
## Method: SubProcessTask.processOutputs

### Description
Optional programmatic hook invoked on the parent after the child Process completes successfully and after [SubProcessTask.stateUpdates](#attr-subprocesstaskstateupdates) have been applied. Use this when caller-side post-processing can't be expressed declaratively - for example merging the child's history entry into the parent process's history, or normalizing output shape before downstream tasks read it.

Modifications to `process.state` made here are visible to subsequent tasks. The return value is ignored.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [SubProcessTask](#type-subprocesstask) | false | — | this task |
| process | [Process](#type-process) | false | — | the calling (parent) process |
| output | [Any](#type-any) | false | — | the child's validated output |
| state | [Record](#type-record) | false | — | the parent's current `process.state` |

---
