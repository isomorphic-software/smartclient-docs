# AUN Documentation

[← Back to API Index](../main.md)

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
## Attr: AUN.goal

### Description
The end-user goal that AUN should try to accomplish (e.g., "Create an order and verify it appears").

**Flags**: IR

---
## Method: AUN.getNavigationGraph

### Description
Return the current navigation graph built during exploration.

### Returns

`[Object](../main.md#type-object)` — Navigation graph with nodes and edges

---
## Method: AUN.generateTest

### Description
Generate an AutoTest script from the recorded exploration path.

### Returns

`[String](#type-string)` — AutoTest script

---
## Method: AUN.start

### Description
Start the AUN exploration workflow. Begins with the "analyze" task and continues until the goal is achieved, maxSteps is reached, or a loop is detected.

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

When enabled, AUN will store all prompts sent to the AI and responses received in `state._conversationLog` for later export via [AUN.exportMarkdownLog](#method-aunexportmarkdownlog).

This works by wrapping the AI task execution to capture inputs and outputs. Must be called before starting the AUN workflow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| options | [Object](../main.md#type-object) | false | — | Configuration options for conversation logging |

---
## Method: AUN.exportMarkdownLog

### Description
Export AUN conversation log as markdown with prompts and AI responses.

Returns a formatted markdown document showing the conversation between AUN and the AI, including prompts sent and responses received, with step numbers in headers.

Requires [AUN.enableConversationLogging](#method-aunenableconversationlogging) to be called before starting the workflow.

Supports selective omission of content sections via options parameter:

*   `omitUISummary` - Replace UI hierarchy with placeholder
*   `omitActions` - Replace available actions list with placeholder
*   `omitIntroPrompt` - Replace global CoTProcess intro with placeholder
*   `omitTaskPrompt` - Replace task-specific prompt with placeholder

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| options | [Object](../main.md#type-object) | false | — | Configuration options for log export |

### Returns

`[String](#type-string)` — Markdown-formatted conversation log

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
