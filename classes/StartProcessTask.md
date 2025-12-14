# StartProcessTask Documentation

[← Back to API Index](../reference.md)

---

## Class: StartProcessTask

*Inherits from:* [ScriptTask](ScriptTask.md#class-scripttask)

### Description
Task that executes another [Process](Process.md#class-process) inside the current one. A process cannot be embedded within another process as a normal task element. Instead, a StartProcessTask is used to provide the input state, execute the inner process, then write the output back into the calling process state.

---
## Attr: StartProcessTask.process

### Description
The [Process](Process.md#class-process) to be run by this task. Input state is created from [inputFieldList](Task.md#attr-taskinputfieldlist) and container process state is updated from the inner process state using [outputFieldList](Task.md#attr-taskoutputfieldlist).

This property can be an instance of the target process or an ID. For an ID, the process will be looked up in your screen if this task is part of one and, otherwise, it will be looked up globally via [Process.getProcess](Process.md#classmethod-processgetprocess).

**Flags**: IRW

---
## Attr: StartProcessTask.isAsync

### Description
Not applicable to StartProcessTask.

**Flags**: IRW

---
## Method: StartProcessTask.execute

### Description
Not applicable to StartProcessTask.

---
