# CoTInterceptDialog Documentation

[← Back to API Index](../reference.md)

---

## Class: CoTInterceptDialog

*Inherits from:* [MockInterceptDialog](MockInterceptDialog.md#class-mockinterceptdialog)

### Description
A modal dialog that intercepts CoTTask execution, allowing developers to inspect the assembled prompt, view/modify the response fields, and optionally forward to the real AI.

This dialog is shown when [CoTProcess.mockInteractive](CoTProcess.md#attr-cotprocessmockinteractive) or [CoTTask.mockInteractive](CoTTask.md#attr-cottaskmockinteractive) is true. It provides workflow-level debugging that complements the transport-level debugging available via [AI.mockingPolicy](AI.md#classattr-aimockingpolicy).

CoTInterceptDialog extends [MockInterceptDialog](MockInterceptDialog.md#class-mockinterceptdialog) (if available) or Window, providing a structured form editor based on the task's [CoTTask.outputFields](CoTTask.md#attr-cottaskoutputfields).

**Actions:**

*   **Use Response** - Proceed with the values currently in the form
*   **Send to AI** - Call the real AI, then populate the form with its response
*   **Skip** - Proceed without output (task output will have \_skipped:true)
*   **Cancel** - Stop the entire CoT process

### Groups

- CoTMocking

---
## Attr: CoTInterceptDialog.outputFields

### Description
Task's outputFields used to generate the response form.

**Flags**: IR

---
## Attr: CoTInterceptDialog.fullPrompt

### Description
The assembled prompt text that would be sent to the AI. For compatibility, this is an alias for the 'prompt' property from the base class.

**Flags**: IR

---
## Attr: CoTInterceptDialog.mockEntry

### Description
The mockData entry for this task, if available during replay.

**Flags**: IR

---
## Attr: CoTInterceptDialog.responseCallback

### Description
Callback invoked when the user makes a choice. Signature: `responseCallback(response, action)` where action is "use", "skip", or "cancel".

**Flags**: IR

---
## Attr: CoTInterceptDialog.process

### Description
The CoTProcess that owns the task.

**Flags**: IR

---
## Attr: CoTInterceptDialog.task

### Description
The CoTTask being intercepted.

**Flags**: IR

---
