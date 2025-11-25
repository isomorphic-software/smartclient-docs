# CoTTask Documentation

[← Back to API Index](../main.md)

---

## Class: CoTTask

*Inherits from:* [Task](Task.md#class-task)

### Description
Performs a call to an AI (LLM) and processes the results.

Provides declarative support for prompt assembly, AI-driven "transitions" to other states, validation & retries, storage of AI-generated results, and other features designed to make definitions of Chain-of-Thought (CoT) AI workflows as simple & declarative as possible.

`CoTTask` is typically used within a [CoTProcess](CoTProcess.md#class-cotprocess), which is a simple subclass of [Process](Process.md#class-process) that can coordinate with `CoTTask` on things like common sections of prompts that are used in multiple CoTTasks. However, CoTTask can also be used within a normal Process.

#### Overview
CoTTask:

1.  assembles a prompt, typically in collaboration with a CoTProcess , such that only [taskPrompt](#taskprompt) is set on the task. This includes automatic prompt generation regarding [transitions](#transitions), [CoTProcess.history](CoTProcess.md#attr-cotprocesshistory) and [validation errors](#outputds) in the event of a retry.
2.  contacts the configured LLM, which can be the [AI.defaultAIEngineId](#aidefaultaiengineid) or can be specified as [task.aiEngineId](#attr-cottaskaiengineid) or [process.aiEngineId](CoTProcess.md#attr-cotprocessaiengineid).
3.  processes the AI response, in particular executing AI-driven [transitions](#transitions) to other states, applying [validation](#outputfields), and [auto-retrying](#maxretries) if validation fails
4.  for a successful response, can declaratively store results ([stateUpdates](#stateupdates)) and can invoke custom processing ([processOutputs](#method-processoutputs))
5.  after success, transitions to another task in the standard `Task` manner of checking [nextElement](#nextelement) or membership in a [sequence](Process.md#attr-processsequences), with a special fallback of returning to the calling task or to [CoTProcess.defaultReturnTask](CoTProcess.md#attr-cotprocessdefaultreturntask) if configured

Each of these phases is discussed in more detail below. As a running example, we'll use the following overall process: a small CoT designed to iteratively add fields to a DataSource definition to make the DataSource capable of a developer-specified use case (specified as [process.goal](#processgoal)):
```
 isc.CoTProcess.create({
   ID: "dsBuilder",
   introPrompt: "You assist in building a SmartClient DataSource to match the user's goal." +
          "The current DataSource definition is\n: ${json(state.currentDS)}\\n",
   goal: "Add fields needed for date-range order search",
   state: { currentDS: { fields: [ ... fields that exist before running this CoT .. ] } },
   tasks: [
     { ID:"decide",
       transitions : [ { to: "addField" }, { to:"done" } ]
     },
     { ID:"addField", title: "Add Field",
       taskPrompt : "Generate a DataSourceField definition.  You may ... additional details ",
       outputFields: [  fields with validators to check for a valid field definition  ],
       stateUpdates : "currentDS.fields[]",
       nextElement:"decide"
     },
     { ID:"done", title: "Finish" }
   ]
 });
 
```

#### Prompt Assembly

Unless you explicitly set [prompt](#attr-cottaskprompt), to provide the complete prompt for this task, the prompt is assembled using a series of prompt fragments from the surrounding [CoTProcess](CoTProcess.md#class-cotprocess) plus settings on the `task`. Essentially, the AI is given a centrally defined [purpose and progress so far](CoTProcess.md#attr-cotprocessintroprompt), [goal](CoTProcess.md#attr-cotprocessgoal), [background on its recent attempts](../kb_topics/CoTHistory.md#kb-topic-cothistory), [validation errors](#attr-cottaskoutputds) (if in the middle of a retry) and available [transitions](#attr-cottasktransitions) meaning other actions that the AI could choose to take.

Each part of the default prompt also includes modifiable _primer text_ which explains to the AI what each of these standard outputs means. For example, the [CoTProcess.errorsPrimer](CoTProcess.md#attr-cotprocesserrorsprimer) explains the format of validation errors to the AI, so that it can attempt corrections.

#### Transitions

Transitions are other states in the CoT that the AI can choose to go to. For example, in the running example of a DataSource builder CoT, there is a "decide" step where the AI can choose to either "addField" or be "done":

```
     { ID:"decide",
       transitions : [ { to: "addField" }, { to:"done" } ]
     },
 
```
A [CoTTransition](../main_2.md#object-cottransition) can declare a [label](CoTTransition.md#attr-cottransitionlabel) to describe the target step. If this is omitted, the target's [description](#attr-cottaskdescription) is used if present, otherwise its [title](#cottasktitle).

As part of default prompt assembly, if `transitions` are defined, the [transitionsPrimer](#transitionsprimer) explains to the AI how to perform a transition (by outputting a particular JSON object). Then the `transitions` themselves are output one at a time using the [transitionsPrimer](#transitionsprimer).

Built-in logic in `CoTTask` recognizes when the AI has picked a `transition` and performs it (via [process.setNextElement(_targetTask_)](Process.md#method-processsetnextelement)). If the AI appears to attempt a transition but it's invalid in some way (bad target task, for example), validation errors are generated and the AI request is retried, up to [maxRetries](#maxretries). This makes transition handling 100% codeless.

The _transitionsPrimer_ tells the AI to generate intent and stepAfter attributes in the JSON output that triggers transitions. These attributes are included in the history to help the AI keep track of what it's doing when, to complete one logic action, it has to perform several tasks in a row. See **History** below.

#### History

The AI contacted by `CoTTask` is assumed to have no working memory, that is, each prompt it receives is the _only_ thing it knows about its task. For a simple CoT like our running example of a DataSource builder, it's sufficient that the [standard prompt template](#attr-cottaskprompt) always outputs the current state of the DataSource being built.

However, in a more complex CoT involving _augmenting_ a DataSource (imagine a _modifyField_ task), the AI might intend to use several `CoTTasks` to accomplish a single logical task. For example, the AI might need to modify two fields to reference each other, but if presented with the modified DataSource definition with the logical task halfway done, it might appear as though one of the fields is simply broken (references a non-existent "displayField", for example), which the AI might then decide to fix.

This can lead to loops, which the history feature helps to prevent.

`history` is maintained as a simple Array of Objects under the "history" property in the [Process.state](Process.md#attr-processstate), which is serialized as JSON in the default prompt, with the [historyPrimer](#historyprimer) before it (to explain history).

Each successful transition automatically adds a history entry including intent and stepAfter. Each successful non-transition output is likewise auto-added to history. Retries are not tracked.

Set [noHistory](#nohistory) to prevent a given task from adding automatic history entries, or [CoTProcess.noHistory](CoTProcess.md#attr-cotprocessnohistory) to disable history tracking for an entire process, such that history is not included in prompts and no history entries are recorded.

#### Validation

For non-transition output by the AI, validation is applied if configured. Validation is done via the same system used for DataSources that perform CRUD operations, so you have all of those features, including [conditional validators](Validator.md#attr-validatorapplywhen), [server-based validators](Validator.md#attr-validatorserveronly) and other features. Declare validation like so:

1.  [outputFields](#outputfields): an Array of DataSourceField
2.  [outputDS](#outputds): a full DataSource definition

Both forms of defining validators can validate nested structures by using [DataSourceField.type](DataSourceField.md#attr-datasourcefieldtype) to refer to the [DataSource.ID](DataSource.md#attr-datasourceid) of another DataSource which describes the nested object.

Note that if you write a CoT that is supposed to produce a record to save to a currently loaded CRUD DataSource, you can simply supply the CRUD DataSource as `outputDS`, and you're done.

If validation fails, the task retries up to [CoTTask.maxRetries](#attr-cottaskmaxretries) (defaulting to [CoTProcess.maxRetries](CoTProcess.md#attr-cotprocessmaxretries)); on exhaustion, the process stops and [Process.finished](Process.md#method-processfinished) is fired with failure=true.

#### Declarative Process State Updates

When AI produces a non-transition result, typically it just needs to be stored to `process.state`, and if so, this can be done declaratively. In our running example, [stateUpdates](#stateupdates) is used to add the AI-generated field to the existing fields Array:

```
 { ID:"addField", title: "Add Field", ... other properties ...
       stateUpdates : "currentDS.fields[]" // the [] appends to an existing Array or creates one if needed
  },
 
```
Shown above is a shorthand format; in general `stateUpdates` is a mapping from a [statePath](../main.md#type-statepath) to a ${TaskInputExpression} or other value.
```
 { ID:"addField", title: "Add Field", ... other properties ...
    stateUpdates : {
       "currentDS.fields[]" : "$outputs"
    }
  },
 
```
If the processing of the AI result is more complicated, you can implement [processOutputs](#method-processoutputs). To achieve the above, you would implement:
```
    processOutputs : function (task, process, outputs, state) {
         this.setState("currentDS.fields[]", outputs);
    }
 
```
Note that `stateUpdates` can declare nested structures, and `TaskInputExpressions` are allowed anywhere in the nested declaration. So for example, let's say our CoT got more complicated and there are multiple ways that fields might be added, but we want to keep track of the last field that was specifically added by the "Add Field" CoT step. We could declare `stateUpdates` like this, in order to maintain an object called "lastCreatedField" as `process.state.lastCreatedField`:
```
    stateUpdates : {
         "currentDS.fields[]" : "$outputs"
         "lastCreatedField" : {
             "fromTask" : "Add Field",
             "fieldName" : "$outputs.name"
         }
    }
 
```
You can also programmatically apply `stateUpdates` at any time (even before outputs have been determined), via [process.applyUpdates(_stateUpdates_)](#processapplyupdates).
#### Default routing and overrides

If a response is not a transition (no top-level `goTo`/`intent`/`stepAfter`), and the task succeeds (no validation errors), the next task is determined by the standard [Process](Process.md#class-process) approach, with some special `CoTTask`/`CoTProcess` behaviors and settings. The next task (or more generally, `ProcessElement`) is:

1.  [nextElement](ProcessElement.md#attr-processelementnextelement) if set on the current `CoTTask`, possibly dynamically if `processOutputs` calls [Process.setNextElement](Process.md#method-processsetnextelement) _\[standard Process behavior\]_
2.  if the current `CoTTask` is declared in a [sequence](Process.md#attr-processsequences), the next element in that sequence _\[standard Process behavior\]_
3.  [CoTProcess.defaultReturnTask](CoTProcess.md#attr-cotprocessdefaultreturntask) on the process, if set. This is useful for simple CoTs that have a single "decision" step that is repeatedly returned to_\[specific to CoTTask / CoTProcess\]_
4.  Return to the calling task - this is useful for CoTs with a "hubs-and-spokes" layout, where there are multiple decision-point "hubs" each of which has several "spoke" leaf tasks _\[specific to CoTTask / CoTProcess\]_

### Groups

- CoT

---
## Attr: CoTTask.maxRetries

### Description
Maximum number of retries for validation failures for this task. If unset, inherits from [CoTProcess.maxRetries](CoTProcess.md#attr-cotprocessmaxretries). A value of 0 disables retries.

**Flags**: IR

---
## Attr: CoTTask.outputFields

### Description
Shorthand for [CoTTask.outputDS](#attr-cottaskoutputds), causing a temporary DataSource to be created to validate AI outputs. See [CoTTask.outputDS](#attr-cottaskoutputds) for details of how validation is performed.

**Flags**: IR

---
## Attr: CoTTask.stateUpdates

### Description
Declarative mapping from [StatePaths](../main.md#type-statepath) to [TaskInputExpressions](../main_2.md#type-taskinputexpression), or just a single StatePath if the entire outputs object should be applied to a single path. When the task completes successfully (no validation errors), each mapping is applied to update [Process.state](Process.md#attr-processstate). Shorthand: a String path means the entire outputs go to that path.

**Flags**: IR

---
## Attr: CoTTask.outputDS

### Description
DataSource (definition or ID) used to validate outputs produced by the AI. Outputs are validated via [DataSource.validateData](DataSource.md#method-datasourcevalidatedata). Nested structures are supported via DataSource field types. If both `outputDS` and `outputFields` are provided, `outputDS` takes precedence.

**Flags**: IR

---
## Attr: CoTTask.transitions

### Description
Advertises allowed next steps. When `$outputs.goTo` names one of these, its inputs are evaluated and delivered as `inputs` to the target task. Transitions whose `visibleWhen` evaluate false are considered unavailable: they are not listed in prompt fragments and selecting them is treated as an invalid transition (validation error).

**Flags**: IR

---
## Attr: CoTTask.errorsPrimer

### Description
Optional task-level override for the [process-level errorsPrimer](CoTProcess.md#attr-cotprocesserrorsprimer), in case a task needs to explain validation errors differently.

**Flags**: IR

---
## Attr: CoTTask.prompt

### Description
Full prompt override for this task. If set, this String is used verbatim and the default prompt assembly, which normally coordinates with a surrounding [CoTProcess](CoTProcess.md#class-cotprocess), is skipped. In most cases you should not set this property directly. Instead, supply a [taskPrompt](#attr-cottasktaskprompt) and let the engine assemble the full prompt (goal, history, errors, transitions, etc). You can replicate the default assembly using [CoTProcess.getPromptPart](CoTProcess.md#method-cotprocessgetpromptpart) and helpers `promptPart()`/`prt()`.

**Flags**: IR

---
## Attr: CoTTask.mockMode

### Description
Per-task control of mocking. When true, this task skips real AI calls and uses [CoTTask.mockOutput](#method-cottaskmockoutput). When false, this task calls the real AI even if [CoTProcess.mockMode](CoTProcess.md#attr-cotprocessmockmode) is true. When null (or unset), the task inherits [CoTProcess.mockMode](CoTProcess.md#attr-cotprocessmockmode).

### Groups

- CoTMocking

**Flags**: IRW

---
## Attr: CoTTask.description

### Description
Human-readable description of this task's purpose. Used when generating prompt output for [CoTTask.transitions](#attr-cottasktransitions). If unset, [CoTTask.title](#cottasktitle) is used instead.

**Flags**: IR

---
## Attr: CoTTask.taskPrompt

### Description
The task's main guidance/content, inserted by the default prompt builder after history and errors. May be a String template (rendered against [CoTPromptScope](../kb_topics/CoTPromptScope.md#kb-topic-cotpromptscope)) or a Function that returns text. In many tasks this is the only property you need to set.

**Flags**: IR

---
## Attr: CoTTask.aiEngineId

### Description
Identifier of the AI engine to use when this task calls an LLM. If unset, inherits from [CoTProcess.aiEngineId](CoTProcess.md#attr-cotprocessaiengineid) if set; otherwise falls back to [AI.defaultAIEngineId](#aidefaultaiengineid). Allows per-task specialization.

**Flags**: IR

---
## Attr: CoTTask.noHistory

### Description
Task-level switch which causes this task to not add automatic history entries.

**Flags**: IR

---
## Method: CoTTask.getPromptContext

### Description
Returns the template scope used to render this task's prompt, including the data and helpers described under [CoTPromptScope](../kb_topics/CoTPromptScope.md#kb-topic-cotpromptscope).

### Returns

`[Object](../main.md#type-object)` — Prompt context object

---
## Method: CoTTask.mockOutput

### Description
Return synthetic AI output for this task when mocking is in effect (see [CoTTask.mockMode](#attr-cottaskmockmode)). If this method is not defined on the task, the framework falls back to [CoTProcess.mockOutput](CoTProcess.md#method-cotprocessmockoutput). The returned value must be a plain Object shaped like normal AI output (e.g., may include {goTo,intent,stepAfter} for transitions, or fields expected by [CoTTask.outputDS](#attr-cottaskoutputds)/[CoTTask.outputFields](#attr-cottaskoutputfields)).

### Returns

`[Object](../main.md#type-object)` — Fake AI output to be processed as if returned by the model.

### Groups

- CoTMocking

---
## Method: CoTTask.processOutputs

### Description
Programmatic hook to handle non-declarative results. Called after parsing and (if declared) validation, and before routing. Use this when the AI returns something that should be applied imperatively, or when you don't want to declare `stateUpdates`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [CoTTask](#type-cottask) | false | — | This task |
| process | [CoTProcess](#type-cotprocess) | false | — | Owning process |

---
