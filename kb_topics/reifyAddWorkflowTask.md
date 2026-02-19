# Adding Custom Workflow Tasks

[← Back to API Index](../reference.md)

---

## KB Topic: Adding Custom Workflow Tasks

### Description
You can define custom Workflow tasks and add them to the [WorkflowEditor](#class-workfloweditor). This applies whether you are using the Workflow Editor embedded in Reify or as a [standalone component](#class-workfloweditor) (see the *Workflow Editor* and *Custom Task Editor* samples). Custom tasks let designers cover additional use cases within the visual editor without writing code.

The overall steps are:

1.  Create a [ProcessElement](../classes/ProcessElement.md#class-processelement) subclass that performs the desired task.
2.  Build a task editor so users can configure task properties (or skip this step for tasks with no configurable properties).
3.  Register the task with the Workflow Editor via [WorkflowEditor.registerTaskDescriptor](#method-workfloweditorregistertaskdescriptor) (or, in Reify, via `workflowTasks.xml`).

For Reify deployments, a [component schema](componentSchema.md#kb-topic-component-schema) is also needed so the task can be serialized; see **Task Schema (Reify)** below.

**Do I need a custom Workflow task?**

Before building a custom task and editor, consider whether other approaches might work:

1\. _Custom services_ – if you are connecting to an enterprise web service, a custom DataSource may suffice; see [Adding Custom DataSources to Reify](reifyCustomDataSources.md#kb-topic-adding-custom-datasources-to-reify). DataSources can model any network service, not just databases. For example, a proprietary messaging system with inputs like _recipient, subject, message_ can be modelled as a DataSource where those are simply fields and sending is an "add" operation. A custom task may still be worthwhile if you want a specialized editing interface.

2\. _Actions on UI components_ – if your custom components support actions, you can expose them as setter methods (e.g. `setMode(_newMode_)`), add the setter to the Component Schema, and let designers invoke it via the built-in _Set Properties_ workflow task.

**Workflow Task**

A new task must inherit from [ProcessElement](../classes/ProcessElement.md#class-processelement) or a subclass like [ScriptTask](../classes/ScriptTask.md#class-scripttask) or [ComponentTask](../classes/ComponentTask.md#class-componenttask), and override [ProcessElement.executeElement](../classes/ProcessElement.md#method-processelementexecuteelement) (or a subclass-specific method like [ScriptTask.execute](../classes/ScriptTask.md#method-scripttaskexecute)). Return `true` for synchronous completion or `null` for asynchronous (then call `process.start()` when done).

Setting [ProcessElement.typeTitle](../classes/ProcessElement.md#attr-processelementtypetitle) and [ProcessElement.classDescription](../classes/ProcessElement.md#attr-processelementclassdescription) on the class provides default [title](#attr-workflowtaskdescriptortitle) and [description](#attr-workflowtaskdescriptordescription) values, so they don't need to be repeated in the [WorkflowTaskDescriptor](#object-workflowtaskdescriptor).

For Reify, load the task implementation via `globalDependencies.xml` (see ["Adding Custom Components to Reify"](reifyCustomComponents.md#kb-topic-adding-custom-components-to-reify)) or via ["Runtime Customization"](reifyOnSite.md#kb-topic-reify-onsite).

**Task Schema (Reify)**

In Reify, a [component schema](componentSchema.md#kb-topic-component-schema) is needed so the task configuration can be serialized. The schema can be XML or JavaScript and requires:

*   [ID](../classes/DataSource_1.md#attr-datasourceid) = _same as your task class name_
*   [serverType](../classes/DataSource_1.md#attr-datasourceservertype) = "component"
*   [inheritsFrom](../classes/DataSource_1.md#attr-datasourceinheritsfrom) = _superclass name_
*   instanceConstructor = _same as your task class name_

For standalone WorkflowEditor usage without Reify, no schema is needed — tasks are serialized via [getProcessJS()](#method-workfloweditorgetprocessjs) which uses JavaScript reflection.

**Workflow Task Editor**

A task editor lets users configure task properties. If a task has no configurable properties (e.g. a logout task), no editor is needed — simply omit the [editTask()](#method-workflowtaskdescriptoredittask) callback and [editorType](../classes/ProcessElement.md#attr-processelementeditortype).

There are two approaches to building editors:

_Approach 1: Subclass [WorkflowTaskEditor](#class-workflowtaskeditor)_ (or [WorkflowComponentTaskEditor](#class-workflowcomponenttaskeditor) for [ComponentTask](../classes/ComponentTask.md#class-componenttask)-based tasks). Override [getEditorComponents()](#method-workflowtaskeditorgeteditorcomponents), [setEditorValuesFromDefaults()](#method-workflowtaskeditorseteditorvaluesfromdefaults), [getEditorValuesAsDefaults()](#method-workflowtaskeditorgeteditorvaluesasdefaults), and [validate()](#method-workflowtaskeditorvalidate). Set [editorType](../classes/ProcessElement.md#attr-processelementeditortype) on the task class to your editor class name. See the *Custom Task Editor* sample for a working example.

_Approach 2: Provide an [editTask()](#method-workflowtaskdescriptoredittask) callback_ on the [WorkflowTaskDescriptor](#object-workflowtaskdescriptor). This gives complete control — build any UI you like, then call `callback(editNode)` to save or `callback(null)` to cancel.

Several helper classes are available for building advanced property editors: [WorkflowValuesBindingEditor](#class-workflowvaluesbindingeditor), [WorkflowCriteriaBuilder](#class-workflowcriteriabuilder), [WorkflowDynamicValueItem](#class-workflowdynamicvalueitem), and [WorkflowTemplatedTextItem](#class-workflowtemplatedtextitem).

**Registering the Task**

For the [WorkflowEditor](#class-workfloweditor) to show the new task in its task picker, register a [WorkflowTaskDescriptor](#object-workflowtaskdescriptor) via [WorkflowEditor.registerTaskDescriptor](#method-workfloweditorregistertaskdescriptor). To place the task under a custom folder, first call [WorkflowEditor.registerFolderDescriptor](#method-workfloweditorregisterfolderdescriptor) to create the folder, then set [taskPath](#attr-workflowtaskdescriptortaskpath) to the folder's [ID](#attr-workflowtaskdescriptorid). Descriptors can be removed at runtime via [WorkflowEditor.removeTaskDescriptor](#method-workfloweditorremovetaskdescriptor).

In Reify, the easiest approach is to add the descriptor to the default task tree in `[webroot]/tools/visualBuilder/ workflowTasks.xml`, which uses a tree structure similar to the *tree XML loading example*. The properties on each node are documented on [WorkflowTaskDescriptor](#object-workflowtaskdescriptor).

A descriptor can also be registered at runtime via [Reify.registerWorkflowTaskDescriptor](#method-reifyregisterworkflowtaskdescriptor), which is useful for ["Runtime Customization"](reifyOnSite.md#kb-topic-reify-onsite).

---
