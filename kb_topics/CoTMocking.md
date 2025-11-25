# CoTMocking

[← Back to API Index](../main.md)

---

## KB Topic: CoTMocking

### Description
Facilities for testing CoT workflows without contacting an AI engine. Use [CoTProcess.mockMode](../classes/CoTProcess.md#attr-cotprocessmockmode) to set a process-wide default and [CoTTask.mockMode](../classes/CoTTask.md#attr-cottaskmockmode) to opt individual tasks in or out.

**Precedence:** a task's setting overrides the process default:

*   **task.mockMode:true** → this task mocks, even if the process is not mocking.
*   **task.mockMode:false** → this task calls the real AI, even if the process is mocking.
*   **task.mockMode:null** (or unset) → inherit [CoTProcess.mockMode](../classes/CoTProcess.md#attr-cotprocessmockmode).

When mocking is in effect for a task, the framework calls [CoTTask.mockOutput](../classes/CoTTask.md#method-cottaskmockoutput) (if defined), otherwise [CoTProcess.mockOutput](../classes/CoTProcess.md#method-cotprocessmockoutput). The returned Object is processed exactly like real AI output (validation, history, state updates, routing).

### Related

- [CoTProcess.mockOutput](../classes/CoTProcess.md#method-cotprocessmockoutput)
- [CoTTask.mockOutput](../classes/CoTTask.md#method-cottaskmockoutput)
- [CoTProcess.mockMode](../classes/CoTProcess.md#attr-cotprocessmockmode)
- [CoTTask.mockMode](../classes/CoTTask.md#attr-cottaskmockmode)
- [AUN.mockMode](../classes/AUN.md#attr-aunmockmode)

---
