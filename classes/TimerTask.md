# TimerTask Documentation

[← Back to API Index](../reference.md)

---

## Class: TimerTask

*Inherits from:* [Task](Task.md#class-task)

### Description
A server-side task that pauses workflow execution for a specified duration or until a specific time. When a TimerTask is encountered, the process suspends and creates a wfWait record with type "TIMER" and a resumeAfter timestamp.

**Timer Expiration Mechanism**

For timers to trigger automatically, a background scheduler must periodically check for expired timers. This can be implemented as:

*   A Java ScheduledExecutorService that polls wfWait for expired TIMER records
*   A database job that runs periodically
*   Integration with an external scheduler like Quartz

The polling query would be:

```
 SELECT * FROM wfWait
 WHERE type = 'TIMER' AND status = 'OPEN' AND resumeAfter <= NOW()
 
```

For each expired timer, the scheduler should:

1.  Update the wfWait record to status = 'TRIGGERED'
2.  Load the workflow instance state from wfInstance
3.  Create a Process, restore state, and call resume()

---
## Attr: TimerTask.waitDataSource

### Description
DataSource to use for persisting wait records.

**Flags**: IR

---
## Attr: TimerTask.resumeAfter

### Description
Specific date/time at which to resume workflow execution. Can be a Date object or a dynamic expression like "$scheduledTime" referencing process state. Either duration or resumeAfter must be specified.

**Flags**: IR

---
## Attr: TimerTask.duration

### Description
Duration to wait before continuing workflow execution. Can be specified as:

*   ISO 8601 duration format: "PT1H" (1 hour), "PT30M" (30 minutes), "P1D" (1 day)
*   Number of milliseconds as string: "60000" (1 minute)

Either duration or resumeAfter must be specified.

**Flags**: IR

---
