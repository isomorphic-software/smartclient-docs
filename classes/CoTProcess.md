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

*   Engine selection: [CoTProcess.aiEngineId](#attr-cotprocessaiengineid) (tasks may override with [CoTTask.aiEngineId](CoTTask.md#attr-cottaskaiengineid); system default [AI.defaultEngineId](AI.md#classattr-aidefaultengineid))  
    
*   Retry policy: [CoTProcess.maxRetries](#attr-cotprocessmaxretries) (task override [CoTTask.maxRetries](CoTTask.md#attr-cottaskmaxretries)); exhaustion semantics in [AIRetriesExhausted](../kb_topics/AIRetriesExhausted.md#kb-topic-airetriesexhausted)  
    
*   Execution models overview: [CoTExecutionModels](../kb_topics/CoTExecutionModels.md#kb-topic-cotexecutionmodels)  
    
*   CoTTask step authoring: [CoTTask](CoTTask.md#class-cottask)

### Groups

- CoT

---
## ClassAttr: CoTProcess.defaultCaptureMockData

### Description
When true, the class-level capture session is armed: every running [CoTProcess](#class-cotprocess) that does _not_ explicitly opt out via its own [CoTProcess.captureMockData](#attr-cotprocesscapturemockdata) flag captures AI responses, both into the per-instance [CoTProcess.mockData](#attr-cotprocessmockdata) array and as flat entries in [CoTProcess.defaultMockSteps](#classattr-cotprocessdefaultmocksteps) - so a single test can capture an entire feature tree of nested sub-processes (see [CoTProcess.armCapture](#classmethod-cotprocessarmcapture)) without enumerating sub-process IDs.

Most callers should use the [armCapture()](#classmethod-cotprocessarmcapture) / [disarm()](#classmethod-cotprocessdisarm) helpers rather than setting this flag directly; see [CoTMocking](../kb_topics/CoTMocking.md#kb-topic-cotmocking).

### Groups

- CoTMocking

**Flags**: IRW

---
## ClassAttr: CoTProcess.defaultMockSteps

### Description
Class-level mock-replay payload as a flat global sequence of step entries covering an entire tree of nested CoTProcesses. Each entry has the shape `{processKey, taskID, aiResponse, timestamp, delay?}`. The `processKey` is the running process's `ID` for cached singletons, or its leaf class name for anonymous transient processes. The optional numeric `delay` overrides [CoTProcess.defaultMockReplayDelay](#classattr-cotprocessdefaultmockreplaydelay) for that one step (set to `0` to run that step synchronously).

When set and [CoTProcess._mockSessionMode](#cotprocess_mocksessionmode) is `"replay"`, every running CoTTask is matched against the entry at [CoTProcess._stepCursor](#cotprocess_stepcursor) by the `(processKey, taskID)` tuple. A match yields the entry's `aiResponse` as the synthesized AI output and advances the cursor; a mismatch is a hard failure that terminates the run with a diagnostic. Strict global ordering is intentional: any change to the CoT workflow (task reorder, sub-process moved, extra/missing invocation) surfaces as a divergence rather than silent wrong-data consumption.

Most callers should use the [armReplay()](#classmethod-cotprocessarmreplay) helper rather than setting this directly.

### Groups

- CoTMocking

**Flags**: IRW

---
## ClassAttr: CoTProcess.defaultMockInteractive

### Description
Global default for [CoTProcess.mockInteractive](#attr-cotprocessmockinteractive). When a CoTProcess instance has `mockInteractive: null` (the default), this class-level setting is used.

This allows developers to enable interactive mocking globally for all CoT processes (including built-in features like InstantUI) without needing to intercept process creation:

```
 isc.CoTProcess.defaultMockInteractive = true;
 
```

### Groups

- CoTMocking

**Flags**: IRW

---
## ClassAttr: CoTProcess.defaultMockReplayDelay

### Description
Default delay (in milliseconds) inserted before each mocked CoTTask response is processed - both during a class-level replay session (see [CoTProcess.armReplay](#classmethod-cotprocessarmreplay)) and when a single CoTProcess is run in mock mode via per-instance [CoTProcess.mockMode](#attr-cotprocessmockmode) / [CoTProcess.mockData](#attr-cotprocessmockdata). Models a realistic AI-response cadence for demos, capture/replay walkthroughs, and offline development - mirroring [AI.spoofedResponseDelay](#aispoofedresponsedelay) at the lower-level AI spoofing layer.

A per-step `delay` field on a captured bag entry, when set to a number, overrides this class default for that one step. Set the class default (or a per-step override) to `0` to run mocks synchronously - recommended for unit tests that drive the coordinator directly.

### Groups

- CoTMocking

**Flags**: IRW

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

For multi-process bags spanning a tree of nested sub-processes, see [CoTProcess.defaultMockSteps](#classattr-cotprocessdefaultmocksteps) / [CoTProcess.armReplay](#classmethod-cotprocessarmreplay).

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
## Attr: CoTProcess.pauseAtTaskBoundaries

### Description
When true (the default), pause requests take effect at task boundaries rather than interrupting mid-task. This ensures consistent state.

**Flags**: IRW

---
## Attr: CoTProcess.defaultTaskConstructor

### Description
Name of the default Task subclass to use when auto-constructing plain Objects declared within this process. Plain objects become a [CoTTask](CoTTask.md#class-cottask) by default, unless they specify their own `_constructor`.

**Flags**: IR

---
## Attr: CoTProcess.captureErrors

### Description
If true, the process will catch top-level exceptions during execution and report them via [CoTProcess.getLastError](#method-cotprocessgetlasterror) instead of throwing them. This allows the runner to gracefully handle crashes.

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

For coordinated capture across a tree of nested sub-processes (without enumerating each sub-process by ID), see [CoTProcess.armCapture](#classmethod-cotprocessarmcapture).

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
## Attr: CoTProcess.stepTimeout

### Description
Maximum time (in ms) allowed for a single step (AI request + processing) before triggering an AI\_NETWORK\_TIMEOUT error.

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
## Attr: CoTProcess.maxSteps

### Description
Maximum number of total steps allowed for the process before triggering a STEP\_LIMIT\_EXCEEDED error.

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

For class-level coordinated capture/replay across nested sub-processes, see [CoTProcess.armReplay](#classmethod-cotprocessarmreplay) and [CoTProcess.defaultMockSteps](#classattr-cotprocessdefaultmocksteps).

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
## Attr: CoTProcess.asyncOperation

### Description
When this process is used as an async operation (via getAsyncOperation() or asyncStart()), this property holds the PausableAsyncOperation instance that manages pause/resume/cancel semantics and the result Promise.

**Flags**: R

---
## Attr: CoTProcess.mockInteractive

### Description
When true, displays an interactive UI before each CoTTask executes, allowing the developer to inspect the prompt, modify the response, or forward to the real AI service.

This is useful for debugging workflow logic and understanding how tasks interact. Unlike [CoTProcess.mockMode](#attr-cotprocessmockmode), which automatically uses recorded responses, mockInteractive pauses for human review at each step.

When both mockMode and mockInteractive are true, the UI is pre-populated with the mockData response (if available) but still pauses for review.

Individual tasks can override this setting via [CoTTask.mockInteractive](CoTTask.md#attr-cottaskmockinteractive).

When null (the default), the class-level [CoTProcess.defaultMockInteractive](#classattr-cotprocessdefaultmockinteractive) setting is used. This allows enabling interactive mocking globally without needing to intercept process creation.

### Groups

- CoTMocking

**Flags**: IRW

---
## Attr: CoTProcess.promptModeNoData

### Description
Partial prompt mode omitting large data structures while keeping all logic/text.

Uses truncation for history and errors to limit size without hiding logic. Best for: "Show prompt structure without 100KB of JSON blobs"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: CoTProcess.systemPrompt

### Description
The system message sent to the AI engine. If not set, a default generic SmartClient-context message is used (see [CoTTask._getMessages](#method-cottask_getmessages)).

This is distinct from [CoTProcess.introPrompt](#attr-cotprocessintroprompt) which is prepended to the user message content. The systemPrompt is sent as a separate system-role message to the AI, which most models treat as high-priority instructions.

The framework convention for CoT processes is to populate `systemPrompt` with a step delimiter followed by a newline and a one-line persona / role priming sentence, so that captured request transcripts are easy to scan and the AI receives consistent high-priority role instructions in the system slot:

```
 systemPrompt: "*** ${task.ID} step ***\nYou are ..."
 
```
Can be a template string with `${...}` expressions evaluated against the [prompt scope](../kb_topics/CoTPromptScope.md#kb-topic-cotpromptscope).

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
## Attr: CoTProcess.paused

### Description
True if this process is currently paused.

**Flags**: R

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
Identifier of the AI engine to use for all tasks in this process, unless overridden per-task by [CoTTask.aiEngineId](CoTTask.md#attr-cottaskaiengineid). If unset, tasks fall back to the system-wide default [AI.defaultEngineId](AI.md#classattr-aidefaultengineid).

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
## Attr: CoTProcess.asyncOperationParams

### Description
Optional parameters to pass to the PausableAsyncOperation when created. Can include a cancellationController for external cancellation control.

**Flags**: IRW

---
## ClassMethod: CoTProcess.disarm

### Description
End the current class-level mock-capture or mock-replay session and return to `"idle"`. Reverts any per-instance `captureMockData` flips that [CoTProcess.armCapture](#classmethod-cotprocessarmcapture) made on cached singletons, but does _not_ clear per-instance `mockData` arrays that were populated by the session - those remain available for inspection.

### Groups

- CoTMocking

---
## ClassMethod: CoTProcess.armReplay

### Description
Begin a class-level mock-replay session using a bag previously produced by [CoTProcess.dumpCapturedMockData](#classmethod-cotprocessdumpcapturedmockdata). Installs the bag's flat step sequence as [CoTProcess.defaultMockSteps](#classattr-cotprocessdefaultmocksteps) and resets the class step cursor. Replay is enforced strictly: every running CoTTask is matched against the next step's `(processKey, taskID)` tuple. Any divergence (task reorder, sub-process skipped, sub-process moved to a different parent step, replay running longer than capture) is a hard failure that terminates the run with a diagnostic naming both expected and actual coordinates.

No-ops with a warning if a capture session is already armed; call [CoTProcess.disarm](#classmethod-cotprocessdisarm) first. Bags whose `formatVersion` does not match the current implementation are also rejected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| bag | [Object](../reference.md#type-object) | false | — | Bag previously produced by [CoTProcess.dumpCapturedMockData](#classmethod-cotprocessdumpcapturedmockdata). |

### Groups

- CoTMocking

---
## ClassMethod: CoTProcess.armCapture

### Description
Begin a class-level mock-capture session. Every [CoTProcess](#class-cotprocess) that subsequently runs - including nested children invoked via [SubProcessTask](SubProcessTask.md#class-subprocesstask) - records its AI responses, both into the per-instance [CoTProcess.mockData](#attr-cotprocessmockdata) array (existing behavior) and as flat `{processKey, taskID, aiResponse, timestamp}` entries in a class-level global step sequence. `processKey` is `process.ID` for cached singletons, falling back to the leaf class name for anonymous transient parents.

Use [CoTProcess.dumpCapturedMockData](#classmethod-cotprocessdumpcapturedmockdata) to retrieve a serializable bag covering the entire feature tree, then [CoTProcess.armReplay](#classmethod-cotprocessarmreplay) on a later run to replay it. Call [CoTProcess.disarm](#classmethod-cotprocessdisarm) between sessions.

No-ops with a warning if a replay session is already armed; call [CoTProcess.disarm](#classmethod-cotprocessdisarm) first.

### Groups

- CoTMocking

---
## ClassMethod: CoTProcess.dumpCapturedMockData

### Description
Return a serializable bag of every AI response captured since [CoTProcess.armCapture](#classmethod-cotprocessarmcapture) was called, suitable for later use with [CoTProcess.armReplay](#classmethod-cotprocessarmreplay).

Safe to call any time during or after a capture session. Calling outside a capture session returns a bag whose `steps` array is empty.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rootKey | [String](#type-string) | true | — | Informational only - identifies the entry-point process so a viewer can label the tree by root. Replay does not require it. |

### Returns

`[Object](../reference.md#type-object)` — Bag with shape `{formatVersion, captured, rootKey?, steps}` where `steps` is an array of `{processKey, taskID, aiResponse, timestamp}` entries in capture order. Each step may be hand-edited to add an optional numeric `delay` field that overrides [CoTProcess.defaultMockReplayDelay](#classattr-cotprocessdefaultmockreplaydelay) for that one step at replay time.

### Groups

- CoTMocking

---
## Method: CoTProcess.getPromptPart

### Description
Returns a named prompt fragment or concatenation of fragments for inclusion in task prompts. Built-in names:

*   **"goal"** – primer from [CoTProcess.goalPrimer](#attr-cotprocessgoalprimer), then [CoTProcess.goal](#attr-cotprocessgoal).
*   **"history"** – primer from [CoTProcess.historyPrimer](#attr-cotprocesshistoryprimer), then recent entries (omitted if [noHistory](#attr-cotprocessnohistory) is true)
*   **"transitions"** – [CoTProcess.transitionsPrimer](#attr-cotprocesstransitionsprimer) followed by the current task's transitions
*   **"errors"** – primer from [CoTProcess.errorsPrimer](#attr-cotprocesserrorsprimer) (or [CoTTask.errorsPrimer](CoTTask.md#attr-cottaskerrorsprimer)), then current validation errors if any
*   **"outputFormat"** – auto-generated "respond in this format" section built from the current task's [CoTTask.outputFields](CoTTask.md#attr-cottaskoutputfields) / [CoTTask.outputDS](CoTTask.md#attr-cottaskoutputds). Renders field name, type, required flag, `description`, and enumerated `valueMap`. Returns empty when the current task has no output schema.
*   **"goalData"** – the raw [CoTProcess.goal](#attr-cotprocessgoal) value.

Names matching keys in [CoTProcess.optionalPrompts](#attr-cotprocessoptionalprompts) return that text. Pass an Array of names to concatenate multiple parts. Set `omitNewlines` to true to omit surrounding newlines.

A task can suppress any of these named parts by setting [CoTTask.partialPrompt](CoTTask.md#attr-cottaskpartialprompt) with an `omit` array; names listed there resolve to the empty string. This lets a task opt out of an auto-generated part (e.g. `"outputFormat"`) when its format is too conditional to express via field metadata.

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
## Method: CoTProcess.isCanceled

### Description
Returns true if this process has been canceled.

### Returns

`[Boolean](#type-boolean)` — —

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
## Method: CoTProcess.asyncStart

### Description
Starts the process and returns a Promise for the result. This is a convenience method that combines getAsyncOperation().asyncGetResult() with start().

### Returns

`[Promise](#type-promise)` — Promise that resolves with the process result or rejects on error/cancel

---
## Method: CoTProcess.finishEarly

### Description
Cancels this process with the special "early finish" disposition: the wrapped operation reports the partial result with `earlyFinish:true` rather than a generic cancellation. Subclasses override the result-shaping hook (`_getEarlyFinishResultProperties()`) when they need to surface domain-specific partial-state alongside the cancellation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| initiator | [Initiator](#type-initiator) | true | — | Who initiated the early finish |

### See Also

- [PausableAsyncOperation.cancel](#method-pausableasyncoperationcancel)

---
## Method: CoTProcess._buildSuccessResult

### Description
Builds the success result object to post to the async operation. Subclasses override to provide appropriate result format.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Object](../reference.md#type-object) | false | — | The final process state |
| output | [Any](#type-any) | true | — | The Process's validated output; see [Process.getOutput](Process.md#method-processgetoutput). |

### Returns

`[AsyncOperationResult](#type-asyncoperationresult)` — The success result

---
## Method: CoTProcess.handlePaused

### Description
Observable notification that this process has been paused. Fires when the underlying PausableAsyncOperation reports a pause; consumers (such as PauseResumeDialog) can observe this method on the process directly to update UI state without reaching into getAsyncOperation().

---
## Method: CoTProcess.processingElement

### Description
Observable method called before each element (task) begins execution. Override or observe to show progress UI.

Callers can access:

*   element.ID: Task identifier (e.g., "determineIsNew", "addComponent")
*   element.title: Human-readable task name
*   process.state.\*: Current state including pendingIntent, pendingComponentType, etc.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [ProcessElement](#type-processelement) | false | — | The element about to execute |
| process | [CoTProcess](#type-cotprocess) | false | — | The process instance (for accessing state) |

---
## Method: CoTProcess.unpause

### Description
Resumes a paused process.

### Returns

`[Boolean](#type-boolean)` — true if was paused and is now resumed

### See Also

- [PausableAsyncOperation.unpause](#method-pausableasyncoperationunpause)

---
## Method: CoTProcess._buildFailureResult

### Description
Builds the failure result object to post to the async operation. Subclasses override to provide appropriate result format.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| failure | [ProcessFailure](#type-processfailure) | false | — | the failure record |

### Returns

`[AsyncOperationResult](#type-asyncoperationresult)` — The failure result

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
Pass a [PartialPromptConfig](../reference_2.md#object-partialpromptconfig) object to customize the mode: // Start with taskPromptOnly, but include history var partial = process.getPartialPrompt({ mode: "taskPromptOnly", add: \["history"\] }); // Start with transitionDebug, also omit errors var partial = process.getPartialPrompt({ mode: "transitionDebug", remove: \["errors"\] });

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

- [PartialPromptConfig](../reference_2.md#object-partialpromptconfig)

---
## Method: CoTProcess.getLastError

### Description
Returns structured error information if the process failed.

### Returns

`[Object](../reference.md#type-object)` — Error object { type, message, stepIndex }

---
## Method: CoTProcess.asyncGetResult

### Description
Returns a Promise for the final result of this process.

### Returns

`[Promise](#type-promise)` — Promise for AsyncOperationResult

### See Also

- [PausableAsyncOperation.asyncGetResult](#method-pausableasyncoperationasyncgetresult)

---
## Method: CoTProcess.failed

### Description
Called when the process terminates via an infrastructure failure - input/output schema mismatch, uncaught exception, AI engine unavailable, cancellation, or ancestor cycle in a [SubProcessTask](SubProcessTask.md#class-subprocesstask). Posts the failure result to the async operation if one exists.

Recoverable errors that are part of the Process's designed output do NOT come through here; they live inside the [finished](#method-cotprocessfinished) result's `output` field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| failure | [ProcessFailure](#type-processfailure) | false | — | the failure record |

---
## Method: CoTProcess.processingElementResult

### Description
Observable method called after each element completes.

Callers can access:

*   element.ID: Task identifier
*   output.\*: Task-specific output (e.g., isNew, uiTitle, paletteNodes)
*   process.state.\*: Updated state after task completion

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [ProcessElement](#type-processelement) | false | — | The element that completed |
| output | [Object](../reference.md#type-object) | false | — | The task's output object |
| process | [CoTProcess](#type-cotprocess) | false | — | The process instance |

---
## Method: CoTProcess.start

### Description
Starts or resumes the process. Overrides Process.start() to check for mock replay failure - if a prior task called [CoTProcess.setMockReplayFailure](#method-cotprocesssetmockreplayfailure), the process terminates immediately rather than continuing to execute tasks against stale mockData.

Also consults the class-level mock-session coordinator (see [CoTProcess.armCapture](#classmethod-cotprocessarmcapture), [CoTProcess.armReplay](#classmethod-cotprocessarmreplay)) to enable capture or pre-load replay data on this run when no explicit per-instance setting exists.

---
## Method: CoTProcess.cancel

### Description
Cancels this process. Any in-progress AI call is aborted, and the result Promise rejects with a canceled result.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | true | — | Reason for cancellation |
| initiator | [Initiator](#type-initiator) | true | — | Who initiated the cancel |

### See Also

- [PausableAsyncOperation.cancel](#method-pausableasyncoperationcancel)

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
## Method: CoTProcess.getAsyncOperation

### Description
Returns the PausableAsyncOperation for this process, creating it if necessary. Use this when you need to pass the operation to UI components like PauseResumeDialog.

### Returns

`[PausableAsyncOperation](#type-pausableasyncoperation)` — The async operation instance

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
## Method: CoTProcess.finished

### Description
Called when the process completes successfully. Posts the success result to the async operation if one exists.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| state | [Object](../reference.md#type-object) | false | — | The final process state |
| output | [Any](#type-any) | true | — | The Process's validated output as computed by [Process.getOutput](Process.md#method-processgetoutput). When no [Process.outputDS](Process.md#attr-processoutputds) / output schema is declared this is the same object as `state`. |

---
## Method: CoTProcess.handleUnpaused

### Description
Observable notification that this process has been unpaused. Counterpart to [CoTProcess.handlePaused](#method-cotprocesshandlepaused).

---
## Method: CoTProcess.pause

### Description
Pauses this process at the next task boundary. If the process is not running or already paused, this has no effect.

### Returns

`[Promise](#type-promise)` — Promise that resolves when unpaused, or rejects if canceled

### See Also

- [PausableAsyncOperation.pause](#method-pausableasyncoperationpause)

---
