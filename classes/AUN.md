# AUN Documentation

[← Back to API Index](../reference.md)

---

## Class: AUN

*Inherits from:* [CoTProcess](CoTProcess.md#class-cotprocess)

### Description
AI UI Navigation (AUN) is a CoT-based workflow engine that explores SmartClient applications to accomplish user-specified goals. AUN uses [UISession](#class-uisession) to track UI state, [AutoTest.getJaccardLocator](#classmethod-autotestgetjaccardlocator) for stable component paths, and Jaccard similarity to detect screen transitions and build a navigation graph.

#### How it works

1.  AUN starts with a user goal (e.g., "create an Order and verify it appears")
2.  At each step, it calls [UISession.getScreenSignature](#method-uisessiongetscreensignature) to understand the current UI state (components, actions, data)
3.  It uses an AI (LLM) to decide what action to take next
4.  It executes the action via [UISession.doCommand](#method-uisessiondocommand), which automatically records the transition in the navigation graph
5.  It compares the new screen to known screens using Jaccard similarity
6.  It repeats until the goal is accomplished or maxSteps is reached

#### Usage
```
 // UISession can be created standalone (will auto-discover UI) or with explicit rootCanvas
 var session = isc.UISession.create({
     rootCanvas: myApp  // optional - omit to auto-discover all top-level canvases
 });

 var aun = isc.AUN.create({
     session: session,
     goal: "Create a new order for customer 'ACME Corp' with 3 items",
     maxSteps: 20
 });

 aun.start();
 
```

#### Key features

*   **Graph-based navigation**: builds a graph of known screens and transitions
*   **Jaccard similarity**: detects when screens are the same, near-equivalent, or different
*   **Loop detection**: avoids revisiting screens unless progress is made
*   **Pathfinding**: can navigate to previously-seen screens via shortest path
*   **Test generation**: successful navigation can be converted to AutoTest scripts

### Groups

- AUN

---
## Attr: AUN.promptModeNavGraphDebug

### Description
Partial prompt mode for debugging navigation graph and screen transitions.

Keeps history and transitions visible to trace navigation paths. Best for: "Why is the navigation graph in this state?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: AUN.loopThreshold

### Description
Maximum number of times AUN can return to the same screen (identified by component structure hash) before considering it stuck in a loop.

This detects when the AI is making actions but not making progress (e.g., repeatedly clicking the same button, navigating back and forth between two screens).

AUN will stop if either this limit is reached OR if [AUN.maxSteps](#attr-aunmaxsteps) is exceeded.

Screen identity is determined by the [UISession](#class-uisession) structure hash of visible components, so different arrangements of the same components count as different screens.

**Flags**: IR

---
## Attr: AUN.mockMode

### Description
If true, AUN runs in mock mode (no real AI calls, uses mockOutput()). Useful for testing and development.

### Groups

- CoTMocking

**Flags**: IRW

---
## Attr: AUN.notificationCallback

### Description
Optional callback function to receive progress notifications during AUN exploration. The callback is invoked with a single string parameter containing the notification message.

Messages match the format used by the mock AutoTest Generator:

*   "Scanning UI" - when analyzing UI state
*   "Focusing on component \[description\]" - when deciding on a target component
*   "Taking action '\[action\]' on component to \[purpose\]" - when executing an action
*   Progress messages during test script generation

Example:

```
 aun.notificationCallback = function(message) {
     console.log("AUN: " + message);
 };
 
```

**Flags**: IRW

---
## Attr: AUN.optionalPrompts

### Description
Optional prompt fragments that can be referenced by tasks.

**Flags**: IR

---
## Attr: AUN.introPrompt

### Description
Intro prompt explaining AUN's role to the AI.

**Flags**: IR

---
## Attr: AUN.promptModeActionSelection

### Description
Partial prompt mode for debugging AI's action selection logic.

Keeps actions and UI context visible while omitting history and transitions. Best for: "Why did the AI choose action X on component Y?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: AUN.tasks

### Description
The workflow tasks that make up the AUN exploration cycle.

**Flags**: IR

---
## Attr: AUN.session

### Description
The UISession instance to use for UI exploration. Must be provided at creation time.

**Flags**: IR

---
## Attr: AUN.maxSteps

### Description
Maximum number of action steps before AUN gives up. This is an absolute limit that prevents truly infinite loops regardless of whether progress is being made.

AUN will stop if either this limit is reached OR if [AUN.loopThreshold](#attr-aunloopthreshold) is exceeded.

This limit is NOT communicated to the AI - it's purely a safety mechanism.

**Flags**: IR

---
## Attr: AUN.promptModeUiScanDebug

### Description
Partial prompt mode for debugging UI scanning and component selection.

Keeps UI summary and focus-related state visible while omitting transitions and errors. Best for: "Why did scanUI choose this component?"

### Groups

- CoTPartialPrompt

**Flags**: IR

---
## Attr: AUN.goal

### Description
The end-user goal that AUN should try to accomplish (e.g., "Create an order and verify it appears").

**Flags**: IR

---
## Method: AUN.getNavigationGraph

### Description
Return the current navigation graph built during exploration.

### Returns

`[Object](../reference.md#type-object)` — Navigation graph with nodes and edges

---
## Method: AUN.generateTest

### Description
Generate an AutoTest script from the recorded exploration path.

### Returns

`[String](#type-string)` — AutoTest script

---
## Method: AUN.getPartialPrompt

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

AUN adds additional modes - see [AUN.getPartialPrompt](#method-aungetpartialprompt).

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
## Method: AUN.start

### Description
Start the AUN exploration workflow. Begins with the "analyze" task and continues until the goal is achieved, maxSteps is reached, or a loop is detected.

---
## Method: AUN.getConversationLog

### Description
Returns the conversation log captured by [AUN.enableConversationLogging](#method-aunenableconversationlogging).

Each entry in the returned array is an object with:

*   `type`: "PROMPT" or "RESPONSE"
*   `stepNumber`: The step number in the workflow
*   `timestamp`: ISO timestamp of when the entry was captured
*   `prompt`: (for PROMPT entries) The prompt sent to the AI
*   `response`: (for RESPONSE entries) The AI response object

### Returns

`[Array](#type-array)` — Array of conversation log entries, or empty array if logging not enabled

---
## Method: AUN.getPlaywrightTest

### Description
Generate a complete Playwright test file from the recorded exploration path. Uses [EventStream.getPlaywrightScript](EventStream.md#classmethod-eventstreamgetplaywrightscript) to convert the session's eventStream into a Playwright test with proper async/await structure, ready to run independently.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetUrl | [String](#type-string) | true | — | URL to visit in beforeEach; defaults to current page. |
| testName | [String](#type-string) | true | — | Name of the test() block; defaults to AUN goal. |
| testDescription | [String](#type-string) | true | — | Description of the test.describe() block; defaults to "AUN Generated Test". |

### Returns

`[String](#type-string)` — Complete Playwright test code ready to save as a .spec.js file

---
## Method: AUN.notify

### Description
Send a notification message via the notificationCallback if one is registered. Used internally to provide progress updates during exploration.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | The notification message |

---
## Method: AUN.enableConversationLogging

### Description
Enable automatic capture of prompts and AI responses for markdown export.

When enabled, AUN will store all prompts sent to the AI and responses received for later export via [AUN.exportMarkdownLog](#method-aunexportmarkdownlog). The captured log can be retrieved via [AUN.getConversationLog](#method-aungetconversationlog).

This works by wrapping the AI task execution to capture inputs and outputs. Must be called before starting the AUN workflow.

#### Partial Prompt Support
Use `partialMode` to capture prompts using a partial mode, reducing log size by omitting large data structures: aun.enableConversationLogging({ partialMode: "noData" });

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| options | [Object](../reference.md#type-object) | false | — | Configuration options for conversation logging |
| options.partialMode | [String](#type-string)|[PartialPromptConfig](#type-partialpromptconfig) | true | — | Partial mode for captured prompts |

---
## Method: AUN.exportMarkdownLog

### Description
Export AUN conversation log as markdown with prompts and AI responses.

Returns a formatted markdown document showing the conversation between AUN and the AI, including prompts sent and responses received, with step numbers in headers.

Requires [AUN.enableConversationLogging](#method-aunenableconversationlogging) to be called before starting the workflow.

#### Partial Prompt Mode
Use `partialMode` to apply a partial prompt mode to exported prompts, which is useful for reducing log size when the full prompts contain large data: var log = aun.exportMarkdownLog({ partialMode: "taskPromptOnly" }); // Or with customization var log = aun.exportMarkdownLog({ partialMode: { mode: "noData", add: \["transitions"\] } }); See [CoTProcess.getPartialPrompt](CoTProcess.md#method-cotprocessgetpartialprompt) for available modes.

#### Legacy Omission Options
Supports selective omission of content sections via options parameter:

*   `omitUISummary` - Replace UI hierarchy with placeholder
*   `omitActions` - Replace available actions list with placeholder
*   `omitIntroPrompt` - Replace global CoTProcess intro with placeholder
*   `omitTaskPrompt` - Replace task-specific prompt with placeholder

Note: When `partialMode` is specified, it takes precedence over the legacy omit\* options for prompt generation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| options | [Object](../reference.md#type-object) | false | — | Configuration options for log export |
| options.partialMode | [String](#type-string)|[PartialPromptConfig](#type-partialpromptconfig) | true | — | Partial prompt mode to apply |

### Returns

`[String](#type-string)` — Markdown-formatted conversation log

### Groups

- CoTPartialPrompt

---
## Method: AUN.mockOutput

### Description
Process-level provider of synthetic AI output used when mocking is in effect.

When [CoTProcess.mockData](CoTProcess.md#attr-cotprocessmockdata) is populated, the default implementation automatically returns the aiResponse from the next AIMockEntry. Override to customize replay behavior or add validation.

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
## Method: AUN.getCypressTest

### Description
Generate a complete Cypress test file from the recorded exploration path. Uses [EventStream.getCypressScript](EventStream.md#method-eventstreamgetcypressscript) to convert the session's eventStream into a Cypress test, ready to run independently.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetUrl | [String](#type-string) | true | — | URL to visit in beforeEach; defaults to current page. |
| testName | [String](#type-string) | true | — | Name of the it() block; defaults to AUN goal. |
| testDescription | [String](#type-string) | true | — | Description of the describe() block; defaults to "AUN Generated Test". |

### Returns

`[String](#type-string)` — Complete Cypress test code ready to save as a .spec.js file

---
