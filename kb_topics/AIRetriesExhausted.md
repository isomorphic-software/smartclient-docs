# AIRetriesExhausted

[← Back to API Index](../reference.md)

---

## KB Topic: AIRetriesExhausted

### Description
A [CoTTask](../classes/CoTTask.md#class-cottask) can automatically retry when its outputs fail validation (via [CoTTask.outputDS](../classes/CoTTask.md#attr-cottaskoutputds)/[CoTTask.outputFields](../classes/CoTTask.md#attr-cottaskoutputfields)) or when [Process.beforeTaskCommit](../classes/Process.md#method-processbeforetaskcommit) returns errors. The retry budget is controlled by [CoTTask.maxRetries](../classes/CoTTask.md#attr-cottaskmaxretries) and, if unset on the task, inherits from [CoTProcess.maxRetries](../classes/CoTProcess.md#attr-cotprocessmaxretries).

A response that is not valid JSON, or that names a `goTo` the task's [CoTTask.transitions](../classes/CoTTask.md#attr-cottasktransitions) do not allow, is retried the same way. Each retry re-runs the task with the problems found included in its prompt. The policy is [CoTProcess.handleOutputValidationFailure](../classes/CoTProcess.md#method-cotprocesshandleoutputvalidationfailure), which subclasses may override.

#### What happens when retries are exhausted
If every attempt fails up to the retry budget:

*   No [CoTTask.stateUpdates](../classes/CoTTask.md#attr-cottaskstateupdates) are committed.
*   The process halts immediately (no fallback routing).
*   [Process.failed](../classes/Process.md#method-processfailed) is fired with a [ProcessFailure](../reference.md#object-processfailure) whose `code` is `"taskOutputValidation"`, whose `message` names the failing task and its last problem, and whose `errors` are the final validation errors.

#### Detecting retry exhaustion
```
 isc.CoTProcess.create({
     ...
     failed : function (failure) {
         if (failure.code == "taskOutputValidation") {
             isc.logWarn("CoT halted: " + failure.message);
         }
     }
 });
 
```

---
