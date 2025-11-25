# AIRetriesExhausted

[← Back to API Index](../main.md)

---

## KB Topic: AIRetriesExhausted

### Description
A [CoTTask](../classes/CoTTask.md#class-cottask) can automatically retry when its outputs fail validation (via [CoTTask.outputDS](../classes/CoTTask.md#attr-cottaskoutputds)/[CoTTask.outputFields](../classes/CoTTask.md#attr-cottaskoutputfields)) or when [Process.beforeTaskCommit](../classes/Process.md#method-processbeforetaskcommit) returns errors. The retry budget is controlled by [CoTTask.maxRetries](../classes/CoTTask.md#attr-cottaskmaxretries) and, if unset on the task, inherits from [CoTProcess.maxRetries](../classes/CoTProcess.md#attr-cotprocessmaxretries).

#### What happens when retries are exhausted
If every attempt fails up to the retry budget:

*   No [CoTTask.stateUpdates](../classes/CoTTask.md#attr-cottaskstateupdates) are committed.
*   The process halts immediately (no fallback routing).
*   [Process.finished(process,lastTask,failure)](../classes/Process.md#method-processfinished) is fired with `lastTask` set to the failing task and `failure` set to `true`.

#### Detecting retry exhaustion
You can observe exhaustion by implementing [Process.finished](../classes/Process.md#method-processfinished) and checking the `failure` flag. In isolation tests that use [runTask()](../classes/Process.md#method-processruntask), the same notification fires on exhaustion; the task's validation errors remain available on the task.
```
 isc.CoTProcess.create({
     ...
     finished : function (proc, lastTask, failure) {
         if (failure) {
             isc.logWarn("CoT halted: retries exhausted in task: " + lastTask.ID);
             // lastTask.errors contains the final validation errors
         }
     }
 });
 
```

---
