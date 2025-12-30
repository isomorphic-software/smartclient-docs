# ProcessElement Documentation

[← Back to API Index](../reference.md)

---

## Class: ProcessElement

### Description
A ProcessElement is an abstract superclass for elements involved in a [Process](Process.md#class-process), such as a [Task](Task.md#class-task) or [XORGateway](XORGateway.md#class-xorgateway).

---
## Attr: ProcessElement.editorType

### Description
Editor type used to edit instances of this type of process element.

**Flags**: IR

---
## Attr: ProcessElement.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)? See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state.

**Flags**: IR

---
## Attr: ProcessElement.description

### Description
Optional description for this specific instance of process element.

**Flags**: IR

---
## Attr: ProcessElement.ID

### Description
Optional ID for this process element, allowing it to be referred to from [Gateways](DecisionGateway.md#class-decisiongateway), or as the [Process.startElement](Process.md#attr-processstartelement). See [ProcessSequence](../reference.md#class-processsequence) and [Process](Process.md#class-process) to understand when this is required or can be omitted.

Unlike [Canvas.ID](Canvas.md#attr-canvasid) a `processElement`'s is a not a globally unique variable, it need only by unique within it's process.

When assigned an ID, a `processElement` can be retrieve via [Process.getElement](Process.md#method-processgetelement).

**Flags**: IR

---
## Attr: ProcessElement.title

### Description
Optional short, descriptive title for this process element. Used by an editor a title for process elements of this type.

**Flags**: IR

---
## Attr: ProcessElement.classDescription

### Description
Optional description of the general nature of the kinds of tasks this this process element performs. Not to be confused with [description](#attr-processelementdescription) which describes what the specific instance of the process element has been configured to do.

For example, the `classDescription` for a task to disable a field might be "disables a field" whereas the `description` for a concrete instance might be "disables the 'shipTo' field in the 'ordering' form".

Used by editor to display additional details along with [title](#attr-processelementtitle).

**Flags**: IR

---
## Attr: ProcessElement.nextElement

### Description
Next [sequence](Process.md#attr-processsequences) or [element](Process.md#attr-processelements) to execute after this one completes.

`nextElement` does not need to be specified on most elements if you use [sequences](Process.md#attr-processsequences).

Note that if there is both a `sequence` and a normal `element` with the same name in the current `Process`, the `sequence` will be used.

**Flags**: IR

---
## Method: ProcessElement.getElementDescription

### Description
Returns a text description of the element derived from the configuration.

If no override is provided by the concrete ProcessElement implementation the [ProcessElement.description](#attr-processelementdescription) or [ProcessElement.ID](#attr-processelementid) is returned.

### Returns

`[String](#type-string)` — the derived element description

---
