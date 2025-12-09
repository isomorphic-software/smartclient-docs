# CoTMocking

[← Back to API Index](../reference.md)

---

## KB Topic: CoTMocking

### Description
Facilities for testing CoT workflows without contacting an AI engine. Use [CoTProcess.mockMode](../classes/CoTProcess.md#attr-cotprocessmockmode) to set a process-wide default and [CoTTask.mockMode](../classes/CoTTask.md#attr-cottaskmockmode) to opt individual tasks in or out.

**Precedence:** a task's setting overrides the process default:

*   **task.mockMode:true** → this task mocks, even if the process is not mocking.
*   **task.mockMode:false** → this task calls the real AI, even if the process is mocking.
*   **task.mockMode:null** (or unset) → inherit [CoTProcess.mockMode](../classes/CoTProcess.md#attr-cotprocessmockmode).

When mocking is in effect for a task, the framework calls [CoTTask.mockOutput](../classes/CoTTask.md#method-cottaskmockoutput) (if defined), otherwise [CoTProcess.mockOutput](../classes/CoTProcess.md#method-cotprocessmockoutput). The returned Object is processed exactly like real AI output (validation, history, state updates, routing).

#### MockData Capture and Replay
For regression testing, you can capture real AI responses during a live run and replay them later without contacting the AI. Set [captureMockData:true](../classes/CoTProcess.md#attr-cotprocesscapturemockdata) to record responses, then use [mockMode:true](../classes/CoTProcess.md#attr-cotprocessmockmode) with the captured [CoTProcess.mockData](../classes/CoTProcess.md#attr-cotprocessmockdata) array for replay.

**Note:** Replay is sensitive to environment differences. See [CoTProcess.captureMockData](../classes/CoTProcess.md#attr-cotprocesscapturemockdata) for details on avoiding false regressions.

### Related

- [CoTProcess.mockOutput](../classes/CoTProcess.md#method-cotprocessmockoutput)
- [CoTProcess.setMockReplayFailure](../classes/CoTProcess.md#method-cotprocesssetmockreplayfailure)
- [CoTTask.mockOutput](../classes/CoTTask.md#method-cottaskmockoutput)
- [AUN.mockOutput](../classes/AUN.md#method-aunmockoutput)
- [CoTProcess.mockMode](../classes/CoTProcess.md#attr-cotprocessmockmode)
- [CoTProcess.captureMockData](../classes/CoTProcess.md#attr-cotprocesscapturemockdata)
- [CoTProcess.mockData](../classes/CoTProcess.md#attr-cotprocessmockdata)
- [CoTTask.mockMode](../classes/CoTTask.md#attr-cottaskmockmode)
- [AUN.mockMode](../classes/AUN.md#attr-aunmockmode)

---
