# CoTProcess Documentation

[← Back to API Index](../reference.md)

---

## Class: CoTProcess

*Inherits from:* [Process](Process.md#class-process)

### Description
Coordinates a Chain-of-Thought workflow built from [CoTTask](CoTTask.md#class-cottask) steps. CoTProcess specifically coordinates with CoTTask by providing default prompt parts (see [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart)) and global handling used by CoTTasks that run inside a CoTProcess (for example, shared goal/context, history visibility, and process-level policies).

#### Authoring: auto-instantiate CoTTasks
CoTProcess overrides [Process.defaultTaskConstructor](Process.md#attr-processdefaulttaskconstructor) so plain Objects in [tasks](Process.md#attr-processtasks) are auto-instantiated as [CoTTask](CoTTask.md#class-cottask). You do not need to specify `_constructor` on each task, so simplified process declarations like the following work:
```
 isc.CoTProcess.create({
   ...
   tasks: [
     { ID:"decide",   title:"Decide Next"       }, // becomes CoTTask
     { ID:"addField", title:"Add Field"         }  // becomes CoTTask
   ]
 });
 
```

#### Shared prompt segments
`CoTTasks` in the process will automatically use shared prompts segments specified on the process as described under [CoTTask.prompt](CoTTask.md#attr-cottaskprompt).

Use [CoTProcess.optionalPrompts](#attr-cotprocessoptionalprompts) for fragments shared by several - but not all - tasks. Those tasks can use [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart) to obtain those prompt segments, including via the in-template helpers `promptPart()` / `prt()`.

#### History
CoTProcess maintains a bounded [history](#attr-cotprocesshistory) list (mirrored to `state.history`) so prompts can include recent AI actions. See [CoTHistory](../kb_topics/CoTHistory.md#kb-topic-cothistory) for what is recorded, how it is stored, and how to include it (for example, `${promptPart('history')}`). Primer text for history is customizable via [CoTProcess.historyPrimer](#attr-cotprocesshistoryprimer).

#### Testing individual steps
Use [runTask()](Process.md#method-processruntask) to enter a single CoTTask with fixed state and/or [Process.ruleScope](Process.md#attr-processrulescope) during development. This is the fastest way to tune a [CoTTask.taskPrompt](CoTTask.md#attr-cottasktaskprompt) and verify validation/state updates without running the whole workflow.

#### Further features

*   Engine selection: [CoTProcess.aiEngineId](#attr-cotprocessaiengineid) (tasks may override with [CoTTask.aiEngineId](CoTTask.md#attr-cottaskaiengineid); system default [AI.defaultAIEngineId](#aidefaultaiengineid))  
    
*   Retry policy: [CoTProcess.maxRetries](#attr-cotprocessmaxretries) (task override [CoTTask.maxRetries](CoTTask.md#attr-cottaskmaxretries)); exhaustion semantics in [AIRetriesExhausted](../kb_topics/AIRetriesExhausted.md#kb-topic-airetriesexhausted)  
    
*   Execution models overview: [CoTExecutionModels](../kb_topics/CoTExecutionModels.md#kb-topic-cotexecutionmodels)  
    
*   CoTTask step authoring: [CoTTask](CoTTask.md#class-cottask)

### Groups

- CoT

---
## Attr: CoTProcess.promptModeMinimal

### Description
Partial prompt mode producing the smallest useful prompt for quick inspection.

Keeps only goal and taskPrompt; omits everything else including large state variables. Best for: "Show me just the essentials" or "Quick overview of prompt structure"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.transitionsPrimer

### Description
Primer text shown before the transitions list when using [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart) with "transitions".

**Flags**: IR

---
## Attr: CoTProcess.mockData

### Description
Array of mock data entries for capture or replay.

**During Capture:** When [CoTProcess.captureMockData](#attr-cotprocesscapturemockdata) is true, this array is automatically populated with entries containing `taskID`, `aiResponse`, and `timestamp` for each AI call.

**During Replay:** When [CoTProcess.mockMode](#attr-cotprocessmockmode) is true and this array is populated, the framework replays responses in sequence, matching each entry's `taskID` against the current task. If the workflow diverges (task IDs don't match), replay fails with a diagnostic error.

### Groups

- CoTMocking

**Flags**: IRW

---
## Attr: CoTProcess.goal

### Description
End-user goal or prompt seed, available in templates as `goal`.

Part of the default [prompt assembly](CoTTask.md#attr-cottaskprompt) for [CoTTasks](CoTTask.md#class-cottask) under this process, available via the shorthand as "prt('goal')" in templates.

**Flags**: IR

---
## Attr: CoTProcess.defaultTaskConstructor

### Description
Name of the default Task subclass to use when auto-constructing plain Objects declared within this process. Plain objects become a [CoTTask](CoTTask.md#class-cottask) by default, unless they specify their own `_constructor`.

**Flags**: IR

---
## Attr: CoTProcess.historyPrimer

### Description
Primer text shown before the history entries when using [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart) with "history".

**Flags**: IR

---
## Attr: CoTProcess.noHistory

### Description
If true, history is not tracked and is omitted from prompts for all tasks in this process.

**Flags**: IR

---
## Attr: CoTProcess.captureMockData

### Description
When true, enables mock data capture mode. During execution, each AI response is recorded in the [CoTProcess.mockData](#attr-cotprocessmockdata) array along with the task ID and timestamp. The captured data can later be used for replay testing by setting [mockMode:true](#attr-cotprocessmockmode) and populating [CoTProcess.mockData](#attr-cotprocessmockdata) with the captured array.

**Environment Sensitivity:** MockData replay assumes the test environment is _exactly_ the same as during capture. Replays can produce false regressions if:

*   **Component IDs change:** If the CoT interacts with SmartClient components that use auto-generated IDs (e.g., `isc_ListGrid_0`), any change to the UI initialization order (additional components created before the test) will cause IDs to differ from the captured values.
*   **Database state changes:** If the CoT modifies a database during capture (creates, updates, or deletes records), subsequent replays against the same database will encounter different data. For example, a captured workflow that finds and edits "Order #123 with status On Hold" will fail on replay if that order no longer exists or has a different status.
*   **External service responses differ:** Any external API calls that return different data on replay will cause workflow divergence.

To avoid false regressions, ensure the test environment is reset to the same state before each replay (e.g., restore database snapshots, use deterministic component IDs via [Canvas.ID](Canvas.md#attr-canvasid), or isolate tests in fresh browser sessions).

**ID Stability via UISession:** CoT processes that use [UISession](#class-uisession) (such as [AUN](AUN.md#class-aun)) benefit from UISession's deterministic ID generation. UISession assigns its own [PathLocalIds](#type-pathlocalid) that are independent of SmartClient's global ID counters, so components created _before_ the session do not affect IDs within the session's scope. See [UISession](#class-uisession) for details on ID stability guarantees.

### Groups

- CoTMocking

**Flags**: IRW

---
## Attr: CoTProcess.promptModeTaskPromptOnly

### Description
Partial prompt mode for debugging task-specific prompt content.

Omits shared boilerplate (introPrompt, history, errors, primers) to focus on what makes this task unique. Best for: "Why is my task asking the wrong question?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.promptModeTransitionDebug

### Description
Partial prompt mode for debugging conditional transition logic between tasks.

Keeps transitions visible while omitting intro and history noise. Best for: "Why did the workflow go to task X instead of Y?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.introPrompt

### Description
The beginning of the AI prompt that is common to all participating [CoTTasks](CoTTask.md#class-cottask) in this process, typically used to explain to AI what role it is going to play, such as: "You are an expert SmartClient developer..."

**Flags**: IR

---
## Attr: CoTProcess.maxRetries

### Description
Maximum number of retries for validation failures when running [CoTTask](CoTTask.md#class-cottask) steps under this process. Tasks may override via [CoTTask.maxRetries](CoTTask.md#attr-cottaskmaxretries). A value of 0 disables retries.

**Flags**: IR

---
## Attr: CoTProcess.promptModeErrorsOnly

### Description
Partial prompt mode focusing on validation and execution errors.

Shows errors and taskPrompt (for context) while omitting most other content. Best for: "Why did validation fail? What error occurred?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.defaultProcessConstructor

### Description
Name of the default Process subclass to use when auto-instantiating nested process objects.

**Flags**: IR

---
## Attr: CoTProcess.mockMode

### Description
Process-wide default for mocking. When true, tasks inherit mocking unless they explicitly set [CoTTask.mockMode](CoTTask.md#attr-cottaskmockmode) to true (force mock) or false (force real). See precedence rules under [CoTMocking](../kb_topics/CoTMocking.md#kb-topic-cotmocking).

### Groups

- CoTMocking

**Flags**: IRW

---
## Attr: CoTProcess.optionalPrompts

### Description
Chunks of AI prompt text that may be shared across multiple [tasks](CoTTask.md#class-cottask) in the process, but which should not appear in _every_ task's AI prompt.

Individual `CoTTasks` can reference `optionalPrompts` by name when constructing that specific task's prompt (for example in [CoTTask.taskPrompt](CoTTask.md#attr-cottasktaskprompt)), by using the `promptPart(_optionalPromptName_)` helper or its shortcut `prt()`.

**Flags**: IR

---
## Attr: CoTProcess.goalPrimer

### Description
Primer text shown before the goal value when using [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart) with "goal".

**Flags**: IR

---
## Attr: CoTProcess.promptModeNoData

### Description
Partial prompt mode omitting large data structures while keeping all logic/text.

Uses truncation for history and errors to limit size without hiding logic. Best for: "Show prompt structure without 100KB of JSON blobs"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.promptModeStateTracking

### Description
Partial prompt mode for tracking state variable changes across steps.

Keeps all state variables and history visible while omitting boilerplate. Best for: "Why is state.X set to this value?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.promptModeHistoryOnly

### Description
Partial prompt mode focusing on action history and continuity.

Shows history and errors while omitting most other content. Best for: "What actions led to the current state?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.historyMaxItems

### Description
Maximum number of entries retained in [history](#attr-cotprocesshistory). Older entries are discarded.

**Flags**: IR

---
## Attr: CoTProcess.defaultReturnTask

### Description
For a [CoTTask](CoTTask.md#class-cottask) embedded in this process, ID of the task to return to after a successful non-transition response when no explicit next step is chosen by normal Process routing.

When a [CoTTask](CoTTask.md#class-cottask) completes without emitting a transition and there is no [nextElement](ProcessElement.md#attr-processelementnextelement) set and the task is not inside a [sequence](Process.md#attr-processsequences), the engine routes to this task (if set).

This is useful for "hub-and-spokes" CoTs where many leaf steps return to a single "decide/plan" hub. If unset, standard Process routing applies (caller return or end of sequence).

**Routing precedence** (first match wins):

1.  [nextElement](ProcessElement.md#attr-processelementnextelement) on the current task (including any change via [process.setNextElement()](Process.md#method-processsetnextelement))
2.  Next element in a [sequence](Process.md#attr-processsequences)
3.  [this defaultReturnTask](#attr-cotprocessdefaultreturntask)
4.  Return to the calling task. This is a special CoTTask behavior designed for multiple "hub and spoke" CoTs

**Flags**: IR

---
## Attr: CoTProcess.aiEngineId

### Description
Identifier of the AI engine to use for all tasks in this process, unless overridden per-task by [CoTTask.aiEngineId](CoTTask.md#attr-cottaskaiengineid). If unset, tasks fall back to the system-wide default [AI.defaultAIEngineId](#aidefaultaiengineid).

Use this to set a consistent model choice for an entire workflow. For fine-grained control, override per task with [CoTTask.aiEngineId](CoTTask.md#attr-cottaskaiengineid).

**Flags**: IR

---
## Attr: CoTProcess.history

### Description
In-memory history entries recorded for this process (most recent last). A bounded mirror is also kept at [state](Process.md#attr-processstate).history.

**Flags**: IR

---
## Attr: CoTProcess.stateHistoryMaxItems

### Description
Maximum number of entries mirrored to [state](Process.md#attr-processstate).history. If null, defaults to [CoTProcess.historyMaxItems](#attr-cotprocesshistorymaxitems).

**Flags**: IR

---
## Attr: CoTProcess.errorsPrimer

### Description
Primer text shown before validation errors when using [CoTProcess.getPromptPart](#method-cotprocessgetpromptpart) with "errors".

**Flags**: IR

---
## Method: CoTProcess.getPromptPart

### Description
Returns a named prompt fragment or concatenation of fragments for inclusion in task prompts. Built-in names:

*   **"goal"** – primer from [CoTProcess.goalPrimer](#attr-cotprocessgoalprimer), then [CoTProcess.goal](#attr-cotprocessgoal).
*   **"history"** – primer from [CoTProcess.historyPrimer](#attr-cotprocesshistoryprimer), then recent entries (omitted if [noHistory](#attr-cotprocessnohistory) is true)
*   **"transitions"** – [CoTProcess.transitionsPrimer](#attr-cotprocesstransitionsprimer) followed by the current task's transitions
*   **"errors"** – primer from [CoTProcess.errorsPrimer](#attr-cotprocesserrorsprimer) (or [CoTTask.errorsPrimer](CoTTask.md#attr-cottaskerrorsprimer)), then current validation errors if any
*   **"goalData"** – the raw [CoTProcess.goal](#attr-cotprocessgoal) value.

Names matching keys in [CoTProcess.optionalPrompts](#attr-cotprocessoptionalprompts) return that text. Pass an Array of names to concatenate multiple parts. Set `omitNewlines` to true to omit surrounding newlines.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| names | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | One or more fragment names |
| omitNewlines | [Boolean](#type-boolean) | false | — | If true, do not surround with newlines |

### Returns

`[String](#type-string)` — Assembled fragment(s)

### Groups

- CoT

---
## Method: CoTProcess.mockOutput

### Description
Process-level provider of synthetic AI output used when mocking is in effect.

When [CoTProcess.mockData](#attr-cotprocessmockdata) is populated, the default implementation automatically returns the aiResponse from the next AIMockEntry. Override to customize replay behavior or add validation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [CoTTask](#type-cottask) | false | — | The task requesting mock output |
| fullPrompt | [String](#type-string) | false | — | The complete prompt that would be sent to the AI |
| mockEntry | [AIMockEntry](#type-aimockentry) | false | — | The AIMockEntry for this step (if in replay mode). Null if not in replay mode or if no mockData is set. |

### Returns

`[Object](../reference.md#type-object)` — Fake AI output. Return a Promise for async mock generation.

The default implementation is equivalent to:

```
 mockOutput: function (task, fullPrompt, mockEntry) {
     return mockEntry ? mockEntry.aiResponse : null;
 }
 
```
When overriding, call `this.Super("mockOutput", arguments)` to get this default replay behavior. A no-op override that just returns the captured response looks like:
```
 mockOutput: function (task, fullPrompt, mockEntry) {
     return this.Super("mockOutput", arguments);
 }
 
```

### Groups

- CoTMocking

---
## Method: CoTProcess.getPartialPrompt

### Description
Generate a partial prompt with specified fragments omitted for debugging/logging.

Partial prompts help isolate specific aspects of AI prompts when troubleshooting workflow issues. They reduce noise from boilerplate, large data structures, and irrelevant context so you can focus on the specific logic being debugged.

#### Using Built-in Modes
Pass a mode name string to use a pre-configured set of omissions. The mode is resolved by looking for `this.promptMode[ModeName]` on the process instance. Available modes in CoTProcess:

*   **taskPromptOnly** - Focus on task-specific prompt; omit shared boilerplate, history, errors. Best for: "Why is my task asking the wrong question?"
*   **transitionDebug** - Keep transitions visible; omit intro and history. Best for: "Why did the workflow go to task X instead of Y?"
*   **stateTracking** - Keep all state variables and history visible. Best for: "Why is state.X set to this value?"
*   **historyOnly** - Focus on action history; omit most other content. Best for: "What actions led to the current state?"
*   **errorsOnly** - Focus on validation/execution errors. Best for: "Why did validation fail?"
*   **minimal** - Smallest useful prompt (goal + taskPrompt only). Best for: "Quick overview of prompt structure"
*   **noData** - Omit large data but keep logic; truncate history/errors. Best for: "Show logic without 100KB JSON blobs"

AUN adds additional modes - see [AUN.getPartialPrompt](AUN.md#method-aungetpartialprompt).

#### Customizing Modes
Pass a [PartialPromptConfig](../reference.md#object-partialpromptconfig) object to customize the mode: // Start with taskPromptOnly, but include history var partial = process.getPartialPrompt({ mode: "taskPromptOnly", add: \["history"\] }); // Start with transitionDebug, also omit errors var partial = process.getPartialPrompt({ mode: "transitionDebug", remove: \["errors"\] });

#### Custom Configuration
For full control, pass a config without a mode: var partial = process.getPartialPrompt({ omit: \["introPrompt", "history"\], omitStateVars: \["currentSummary", "eventStream"\], truncateHistory: 3 });

If a requested mode is not found, a log message is generated and the full prompt is returned (no omissions).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| config | [String](#type-string)|[PartialPromptConfig](#type-partialpromptconfig) | false | — | Mode name string or configuration object |

### Returns

`[String](#type-string)` — The partial prompt with specified omissions applied

### Groups

- CoTPartialPrompt

### See Also

- [PartialPromptConfig](../reference.md#object-partialpromptconfig)

---
## Method: CoTProcess.addHistory

### Description
Add a history entry to [history](#attr-cotprocesshistory) and, if within limits, mirror to state.history. Honors [CoTProcess.noHistory](#attr-cotprocessnohistory). Entries beyond [CoTProcess.historyMaxItems](#attr-cotprocesshistorymaxitems) are discarded; the state mirror obeys [CoTProcess.stateHistoryMaxItems](#attr-cotprocessstatehistorymaxitems) (or historyMaxItems if null).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| entry | [CoTHistoryEntry](#type-cothistoryentry) | false | — | Entry to append |

### Groups

- CoTHistory

---
## Method: CoTProcess.setMockReplayFailure

### Description
Signal a failure during Mock Replay mode. This immediately halts the process and logs a clear explanation of the failure.

Use this in custom mockOutput() or processOutputs() implementations to enforce sanity checks during replay, such as verifying prompt content or state consistency.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errorExplanation | [String](#type-string) | false | — | Human-readable explanation of what went wrong |

### Groups

- CoTMocking

---
