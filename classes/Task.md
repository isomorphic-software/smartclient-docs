# Task Documentation

[← Back to API Index](../reference.md)

---

## Class: Task

*Inherits from:* [ProcessElement](ProcessElement.md#class-processelement)

### Description
A Task is an abstract superclass for [Process](Process.md#class-process) and for all Task types that can be involved in a Process, such as a [ServiceTask](ServiceTask.md#class-servicetask).

---
## Attr: Task.inputFieldList

### Description
List of multiple fields from the [process state](Process.md#attr-processstate) which are provided as input data to this task. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

If [Task.inputField](#attr-taskinputfield) is also specified, it will be implicitly added to the `inputFieldList` if it is not already present.

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.outputFieldList

### Description
List of multiple fields in the [process state](Process.md#attr-processstate) where this task will write outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

If [Task.outputField](#attr-taskoutputfield) is also specified, it will be implicitly added to the `outputFieldList` if it is not already present.

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.outputExpression

### Description
Special expression to write task output directly into a [DataBoundComponent](../reference.md#interface-databoundcomponent). See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.outputField

### Description
Field in the [process state](Process.md#attr-processstate) where this task writes outputs. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
## Attr: Task.inputField

### Description
Field in the [process state](Process.md#attr-processstate) which is provided as input data to this task. See [taskIO](../kb_topics/taskIO.md#kb-topic-task-input--output).

### Groups

- taskIO

**Flags**: IR

---
