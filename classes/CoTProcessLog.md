# CoTProcessLog Documentation

[← Back to API Index](../reference.md)

---

## Class: CoTProcessLog

*Inherits from:* [LogWindow](#class-logwindow)

### Description
Observational running log of a [CoTProcess](CoTProcess.md#class-cotprocess)'s task-by-task progress. Subclass of [LogWindow](#class-logwindow): reuses LogWindow's message rendering, scroll-on-update, and blinking-caret, and adds process-attach behavior. Purely observational - it does not affect process execution and is safe to destroy at any time.

Per task, the log renders rows from two optional templated strings declared on the [CoTTask](CoTTask.md#class-cottask): [CoTTask.logStartMessage](#cottasklogstartmessage) (rendered when the task begins, after [CoTProcess.processingElement](CoTProcess.md#method-cotprocessprocessingelement)), and [CoTTask.logResultMessage](#cottasklogresultmessage) (rendered after [CoTProcess.processingElementResult](CoTProcess.md#method-cotprocessprocessingelementresult)). Both are evaluated through [CoTProcess._renderTemplate](#cotprocess_rendertemplate) with the same ctx the prompt engine uses (`process`, `task`, `state`, plus `output` for the result-side template).

When a task does not declare `logStartMessage` the row falls back to `task.title` (then `task.ID`); when no `logResultMessage` is declared and the task's output carries a `prompt` / `aiMessage`, the row renders a truncated preview of both. An explicit empty-string template suppresses that row entirely.

Attach via [CoTProcessLog.setProcess](#method-cotprocesslogsetprocess): setting a new process detaches the previous one and clears prior messages; setting `null` detaches cleanly. The widget itself is not closed automatically on process completion - the parent app decides whether to leave it open, hide() it after a delay, or destroy it.

---
## Attr: CoTProcessLog.showSystemMessages

### Description
Render rows for process-level lifecycle events (start, finish, failure, cancellation). System rows are styled with [systemStyleName](#systemstylename).

**Flags**: IRW

---
## Attr: CoTProcessLog.showHeader

### Description
CoTProcessLog overrides LogWindow's headerless default so the user has a visible title, drag handle, and dismiss / minimize affordances.

**Flags**: IR

---
## Attr: CoTProcessLog.responsePreviewLength

### Description
Truncation budget for the AI-response preview used by the result-row fallback when a task does not declare a [CoTTask.logResultMessage](#cottasklogresultmessage).

**Flags**: IRW

---
## Attr: CoTProcessLog.showStartMessages

### Description
Render a row each time a task begins (via [CoTProcess.processingElement](CoTProcess.md#method-cotprocessprocessingelement)).

**Flags**: IRW

---
## Attr: CoTProcessLog.intentPreviewLength

### Description
Truncation budget for the optional intent line appended to a start row when `state.pendingIntent` is present (Reify already populates this for AIBuildUI tasks).

**Flags**: IRW

---
## Attr: CoTProcessLog.showResultMessages

### Description
Render a row each time a task completes (via [CoTProcess.processingElementResult](CoTProcess.md#method-cotprocessprocessingelementresult)).

**Flags**: IRW

---
## Attr: CoTProcessLog.title

### Description
Window title shown in the header bar.

**Flags**: IRW

---
## Attr: CoTProcessLog.promptPreviewLength

### Description
Truncation budget for the `prompt` preview used by the result-row fallback when a task does not declare a [CoTTask.logResultMessage](#cottasklogresultmessage).

**Flags**: IRW

---
## Method: CoTProcessLog.setProcess

### Description
Attach this log to a [CoTProcess](CoTProcess.md#class-cotprocess). Detaches from any prior process, clears displayed rows, and starts observing the new one's start / result / lifecycle events. Pass `null` to detach.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [CoTProcess](#type-cotprocess) | false | — | process to observe (or null to detach) |

---
