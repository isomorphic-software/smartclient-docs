# ProcessElement Documentation

[← Back to API Index](../reference.md)

---

## Class: ProcessElement

### Description
A ProcessElement is an abstract superclass for elements involved in a [Process](Process.md#class-process), such as a [Task](Task.md#class-task) or [DecisionTask](DecisionTask.md#class-decisiontask).

---
## Attr: ProcessElement.forceSingle

### Description
Should [multiple record processing](#attr-processelementsupportsmultipleinputrecords) be suppressed for this task instance? This property can be set at any time is checked before executing the task and after each execution during processing of multiple last task output records.

Note that since this property applies to an instance of a task that could be used multiple times in a process (by branching) care should be taken to restore the property value after execution completes. See [ProcessElement.completeElement](#method-processelementcompleteelement) or [ProcessElement.reset](#method-processelementreset).

**Flags**: IRW

---
## Attr: ProcessElement.passThruOutput

### Description
Does this processElement pass through output from the last executed task (i.e. transient state)?

See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state outputs.

Note that this property does not affect the task at all but is an indicator to the user and to the workflow editor of the behavior of the task as coded (See [Process.passThruTaskOutput](Process.md#method-processpassthrutaskoutput)).

**Flags**: IR

---
## Attr: ProcessElement.typeTitle

### Description
Optional short, descriptive title for this process element. Used by an editor as a title for process elements of this type.

**Flags**: IR

---
## Attr: ProcessElement.description

### Description
Optional description for this specific instance of process element.

**Flags**: IR

---
## Attr: ProcessElement.mockMode

### Description
Enable mock mode on the task? If [Process.mockMode](Process.md#attr-processmockmode) is enabled, setting this property to `false` disables mockMode on this task only. Otherwise, mock mode can be enabled on this task by setting it to `true`.

Note that it is up to each task determine what effect mock mode has.

**Flags**: IRW

---
## Attr: ProcessElement.supportsMultipleInputRecords

### Description
Does this processElement support being called multiple times for multiple records in the [last task output](Process.md#method-processsettaskoutput)?

By default a processElement is [executed](#method-processelementexecuteelement) exactly once, however, for a task that can process records from the last task output it can be useful to handle each incoming record individually. Setting this property indicates to the [process](Process.md#class-process) that if the last task output is an array, it should be executed once per value in the array. Normal processing of [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) or use of [Process.getLastTaskOutput](Process.md#method-processgetlasttaskoutput) will have exactly one record except uses of the output for criteria values where the full output is used at once.

Processing of the task can determine that multiple incoming records should not result in multiple calls and set [ProcessElement.forceSingle](#attr-processelementforcesingle). For example, a task that uses last task output for a criteria or for values should set `forceSingle=true` when a criteria is used because multiple calls do not make sense.

**Flags**: IR

---
## Attr: ProcessElement.classDescription

### Description
Optional description of the general nature of the kinds of tasks this this process element performs. Not to be confused with [description](#attr-processelementdescription) which describes what the specific instance of the process element has been configured to do.

For example, the `classDescription` for a task to disable a field might be "disables a field" whereas the `description` for a concrete instance might be "disables the 'shipTo' field in the 'ordering' form".

Used by editor to display additional details along with [typeTitle](#attr-processelementtypetitle).

**Flags**: IR

---
## Attr: ProcessElement.editorType

### Description
Editor type used to edit instances of this type of process element.

**Flags**: IR

---
## Attr: ProcessElement.bindOutput

### Description
When set, the output of the task will be automatically bound to the specified value in the [process state](Process.md#attr-processstate).

See [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) for details on the transient state outputs.

**Flags**: IR

---
## Attr: ProcessElement.ID

### Description
Optional ID for this process element, allowing it to be referred to from [Decisions](MultiDecisionTask.md#class-multidecisiontask), or as the [Process.startElement](Process.md#attr-processstartelement). See [ProcessSequence](../reference.md#class-processsequence) and [Process](Process.md#class-process) to understand when this is required or can be omitted.

Unlike [Canvas.ID](Canvas.md#attr-canvasid) a `processElement`'s is a not a globally unique variable, it need only by unique within it's process.

When assigned an ID, a `processElement` can be retrieve via [Process.getElement](Process.md#method-processgetelement).

**Flags**: IR

---
## Attr: ProcessElement.nextElement

### Description
Next [sequence](Process.md#attr-processsequences) or [element](Process.md#attr-processelements) to execute after this one completes.

`nextElement` does not need to be specified on most elements if you use [sequences](Process.md#attr-processsequences).

Note that if there is both a `sequence` and a normal `element` with the same name in the current `Process`, the `sequence` will be used.

**Flags**: IR

---
## Method: ProcessElement.updateGlobalIDReferences

### Description
Updates references to a global ID within the properties of this process element (i.e. rename). This method is not called as part of workflow execution but is used by [Reify](Reify.md#class-reify) to keep workflow event handlers in sync with ID changes within the screen.

Each processElement or Task that has properties that save global IDs (like a component ID or criteria referencing [ruleContext](Canvas.md#attr-canvasrulescope)) must be able to update its references on demand by overriding this method or defer to its superclass.

There are a number of helper methods to make this easier listed below.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldId | [Identifier](../reference.md#type-identifier) | false | — | the ID being renamed |
| newId | [Identifier](../reference.md#type-identifier) | false | — | the new ID to be assigned |

### Returns

`[Boolean](#type-boolean)` — true if any references were updated; false otherwise

### See Also

- [ProcessElement.updateGlobalIDInValueProperty](#method-processelementupdateglobalidinvalueproperty)
- [ProcessElement.updateGlobalIDInValues](#method-processelementupdateglobalidinvalues)
- [ProcessElement.updateGlobalIDInCriteria](#method-processelementupdateglobalidincriteria)

---
## Method: ProcessElement.updateGlobalIDInCriteria

### Description
Updates [AdvancedCriteria](../reference.md#object-advancedcriteria) [Criterion](../reference_2.md#object-criterion) [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) values containing ruleScope references.

This method is a helper to implement task-specific [ProcessElement.updateGlobalIDReferences](#method-processelementupdateglobalidreferences).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | the criteria to be updated in place |
| oldId | [Identifier](../reference.md#type-identifier) | false | — | the ID being renamed |
| newId | [Identifier](../reference.md#type-identifier) | false | — | the new ID to be assigned |

### Returns

`[Boolean](#type-boolean)` — true if any references were updated; false otherwise

---
## Method: ProcessElement.getEditorType

### Description
Returns the workflow task editor type to be used edit instances of this type of process element. The default implementation returns `this.editorType` but a custom override could determine an editor type based on the property values.

---
## Method: ProcessElement.updateLastElementInValueProperty

### Description
Updates a [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) property value containing $last references. Any implicit reference to the last task is updated to reference a last task of a specified `taskType`.

For example, a value of "$last.sequenceNo" would be replaced with "$last\[fetch\].sequenceNo" if the taskType is "fetch". Existing "$last\[...\]" references are left as-is.

This method is a helper to implement task-specific [ProcessElement.updateLastElementBindingReferences](#method-processelementupdatelastelementbindingreferences).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string) | false | — | the property name to be updated in this task |
| taskType | [String](#type-string) | false | — | the taskType to be used in new reference |

### Returns

`[Boolean](#type-boolean)` — true if any references were update; false otherwise

---
## Method: ProcessElement.updateLastElementInCriteria

### Description
Updates [AdvancedCriteria](../reference.md#object-advancedcriteria) [Criterion](../reference_2.md#object-criterion) [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) values containing $last references. Any implicit reference to the last task is updated to reference a last task of a specified `taskType`.

For example, a value of "$last.sequenceNo" would be replaced with "$last\[fetch\].sequenceNo" if the taskType is "fetch". Existing "$last\[...\]" references are left as-is.

This method is a helper to implement task-specific [ProcessElement.updateLastElementBindingReferences](#method-processelementupdatelastelementbindingreferences).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | the criteria to be updated in place |
| taskType | [String](#type-string) | false | — | the taskType to be used in new reference |

### Returns

`[Boolean](#type-boolean)` — true if any references were update; false otherwise

---
## Method: ProcessElement.getTextFormulaValue

### Description
Resolves a [UserSummary](../reference.md#object-usersummary) value against the current [rule context](Canvas.md#attr-canvasrulescope).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| textFormula | [UserSummary](#type-usersummary) | false | — | the UserSummary value to resolve |
| process | [Process](#type-process) | false | — | the current process |

### Returns

`[String](#type-string)` — the resolved value

---
## Method: ProcessElement.getDynamicValue

### Description
Resolves a dynamic value as [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) or returns the value as-is.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | the value to resolve |
| process | [Process](#type-process) | false | — | the current process |

### Returns

`[String](#type-string)` — the resolved value

---
## Method: ProcessElement.updateGlobalIDInValues

### Description
Updates a set of [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) values containing ruleScope references.

This method is a helper to implement task-specific [ProcessElement.updateGlobalIDReferences](#method-processelementupdateglobalidreferences).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | the object to be updated |
| oldId | [Identifier](../reference.md#type-identifier) | false | — | the ID being renamed |
| newId | [Identifier](../reference.md#type-identifier) | false | — | the new ID to be assigned |

### Returns

`[Boolean](#type-boolean)` — true if any references were updated; false otherwise

---
## Method: ProcessElement.objectReferencesLastTaskOutput

### Description
Does the object have fields that reference the last task output (i.e. $last)?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to be checked |
| process | [Process](#type-process) | false | — | the enclosing process |

### Returns

`[Boolean](#type-boolean)` — true if any field in the object references $last

---
## Method: ProcessElement.reset

### Description
StringMethod called during [Process.reset](Process.md#method-processreset) giving the task a chance to reset any internal state so it can be executed later. See also [ProcessElement.completeElement](#method-processelementcompleteelement).

---
## Method: ProcessElement.executeElement

### Description
Method called by [Process](Process.md#class-process) to have the processElement perform its work. There is no default implementation by ProcessElement, however, all of the system-provided subclasses do implement this method. An implementation or override of this method is one possible customization point. Some classes like [ScriptTask](ScriptTask.md#class-scripttask) perform other means to add customization. For ScriptTask, custom code is expected to handle the [ScriptTask.execute](ScriptTask.md#method-scripttaskexecute) method instead.

Any implementation of this method must return `true` if all the work this element needed to perform was completed. Return `false` if additional work is being performed asynchronously and the process should be paused until element restarts it. Once asynchronous work is complete the task must call [Process.start](Process.md#method-processstart) to restart the workflow with the next task.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the process that is handling the workflow |

### Returns

`[Boolean](#type-boolean)` — return true if all the work this element needed to perform was completed. Return false if additional work is being performed asynchronously and the process should be paused until element restarts it.

---
## Method: ProcessElement.updateGlobalIDInValueProperty

### Description
Updates a [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) property value containing ruleScope references.

This method is a helper to implement task-specific [ProcessElement.updateGlobalIDReferences](#method-processelementupdateglobalidreferences).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string) | false | — | the property name to be updated in this task |
| oldId | [Identifier](../reference.md#type-identifier) | false | — | the ID being renamed |
| newId | [Identifier](../reference.md#type-identifier) | false | — | the new ID to be assigned |

### Returns

`[Boolean](#type-boolean)` — true if any references were updated; false otherwise

---
## Method: ProcessElement.getElementDescription

### Description
Returns a text description of the element derived from the configuration.

If no override is provided by the concrete ProcessElement implementation the [ProcessElement.description](#attr-processelementdescription) is returned.

### Returns

`[String](#type-string)` — the derived element description

---
## Method: ProcessElement.updateLastElementInValues

### Description
Updates a set of [taskInputExpression](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) values containing $last references. Any implicit reference to the last task is updated to reference a last task of a specified `taskType`.

For example, a value of "$last.sequenceNo" would be replaced with "$last\[fetch\].sequenceNo" if the taskType is "fetch". Existing "$last\[...\]" references are left as-is.

This method is a helper to implement task-specific [ProcessElement.updateLastElementBindingReferences](#method-processelementupdatelastelementbindingreferences).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | the object to be updated |
| taskType | [String](#type-string) | false | — | the taskType to be used in new reference |

### Returns

`[Boolean](#type-boolean)` — true if any references were update; false otherwise

---
## Method: ProcessElement.completeElement

### Description
StringMethod called when a processElement completes. Typically used to clear transient state applied to the task while running like [ProcessElement.forceSingle](#attr-processelementforcesingle) so it can be executed again later. See also [ProcessElement.reset](#method-processelementreset).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the containing process |

---
## Method: ProcessElement.updateLastElementBindingReferences

### Description
Update references to a binding $last within properties of this processElement. This method is not called as part of workflow execution but is used by the [WorkflowEditor](#class-workfloweditor) to adjust last task references as new tasks are inserted.

Each processElement or Task that has properties supporting [taskInputExpressions](../kb_topics/taskInputExpression.md#kb-topic-task-input-expressions) using the $last syntax must be able to update its references on demand by overriding this method or defer to its superclass.

There are a number of helper methods to make this easier listed below.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldId | [Identifier](../reference.md#type-identifier) | false | — | the ID being renamed |
| newId | [Identifier](../reference.md#type-identifier) | false | — | the new ID to be assigned |

### Returns

`[Boolean](#type-boolean)` — true if any references were updated; false otherwise

### See Also

- [ProcessElement.updateLastElementInValueProperty](#method-processelementupdatelastelementinvalueproperty)
- [ProcessElement.updateLastElementInValues](#method-processelementupdatelastelementinvalues)
- [ProcessElement.updateLastElementInCriteria](#method-processelementupdatelastelementincriteria)

---
