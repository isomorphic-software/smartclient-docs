# Reify OnSite: Adding Custom Workflow Tasks

[← Back to API Index](../main.md)

---

## KB Topic: Reify OnSite: Adding Custom Workflow Tasks

### Description
You can define your own custom Workflow tasks and add them to Reify's Workflow Editor. This allows your designers to cover additional use cases entirely within the visual design tool, without having to write code.

To create a new Workflow task type and add editing support, the steps are:

1.  Create a subclass of [ProcessElement](../classes/ProcessElement.md#class-processelement) (or one of ProcessElement's subclasses) which performs the desired task, and load that class in Reify.
2.  Create a [component schema](componentSchema.md#kb-topic-component-schema) for the task inheriting from the same superclass schema as the task itself.
3.  Use standard SmartClient UI components to create a UI for editing your new workflow task, called a "task editor", and load this editor in Reify.
4.  Register the new task editor with the Workflow Editor so that new and existing tasks of the new type can be edited.

**Do I need a custom Workflow task?**

Before you start building a custom Workflow task and editor, consider whether other approaches might work as well or nearly as well:

1\. _Custom services_

If you are trying to connect to some kind of enterprise-specific web service, you probably do not need a custom Workflow task but rather just a custom DataSource; see the [Adding Custom DataSources to Reify](reifyCustomDataSources.md#kb-topic-adding-custom-datasources-to-reify) overview instead.

Note that DataSources in Reify can serve as a model for any kind of network service, not just databases that store records. For example, if you have something like a proprietary messaging system with inputs similar to an email (recipient, subject, message text), it may seem like a custom Workflow task is needed, but this could also be modelled as a DataSource where _recipient, subject_, etc are simply DataSource fields, and a message is sent by performing a DataSource "add" operation. However, it _may_ be worthwhile to add a custom Workflow task in this case in order to provide a specialized editing interface, or simply to make it more obvious how to perform the task.

2\. _Actions on UI components_

If you have added custom UI components to Reify, you might want to add custom Workflow tasks for the custom actions that those components support. However, an alternative approach is to make those actions accessible as a "setter method" and have designers invoke the action via the built-in _Set Properties_ workflow task.

For example, you might have a component with two very different display modes, and APIs like `switchToModeOne()` and `switchToModeTwo()`, and you might think of creating a custom Workflow class to call these APIs. However, another approach would be to create a "setter method" like `setMode(_newMode_)`, add it to the Component Schema for the custom component, and have designers change mode via the _Set Properties_ built-in workflow task.

**Workflow Task**

A new workflow task must inherit from [ProcessElement](../classes/ProcessElement.md#class-processelement) or one of its subclasses like [ScriptTask](../classes/ScriptTask.md#class-scripttask) or [ComponentTask](../classes/ComponentTask.md#class-componenttask). The implementation of the task must include an override of [ProcessElement.executeElement](../classes/ProcessElement.md#method-processelementexecuteelement) or other more specific subclass method like [ScriptTask.execute](../classes/ScriptTask.md#method-scripttaskexecute). Be sure to return the correct value to keep the process moving.

By adding [ProcessElement.typeTitle](../classes/ProcessElement.md#attr-processelementtypetitle) and [ProcessElement.classDescription](../classes/ProcessElement.md#attr-processelementclassdescription) property values, the [WorkflowTaskDescriptor.title](#attr-workflowtaskdescriptortitle) and [WorkflowTaskDescriptor.description](#attr-workflowtaskdescriptordescription) properties are not needed when referencing your custom task.

The JavaScript implementation of the task can be loaded in Reify by adding a dependency in the `globalDependencies.xml` file as detailed in ["Adding Custom Components to Reify"](reifyCustomComponents.md#kb-topic-adding-custom-components-to-reify). Alternately, see ["Runtime Customization"](reifyOnSite.md#kb-topic-reify-onsite) for a different means to load the implementation file.

**Task Schema**

A [component schema](componentSchema.md#kb-topic-component-schema) is needed for the new task so that the configuration can be serialized and deserialized correctly. The schema can be declared in XML or in JavaScript code. In either case, the following attributes are required in addition to fields matching each task property:

*   [ID](../classes/DataSource.md#attr-datasourceid) = _same name as your task class_
*   [serverType](../classes/DataSource.md#attr-datasourceservertype) = "component"
*   [inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom) = _class name of your task superclass_
*   instanceConstructor = _same name as your task class_

As with the new workflow task implementation, the schema needs to be loaded into Reify. See the section above for two means of loading the schema.

**Workflow Task Editor**

A task editor is needed for any task that has properties the user can change. If a task doesn't have any properties, like a logout task, there is no need to implement an editor at all. For the [WorkflowTaskDescriptor](#object-workflowtaskdescriptor) created below, don't provide an [editTask()](#method-workflowtaskdescriptoredittask) implementation.

Otherwise, an editor component is needed to edit the properties for an instance of your new workflow task. Custom code that is used by your [editTask()](#method-workflowtaskdescriptoredittask) method should be included for Reify as detailed in Workflow Task above.

To aid in writing custom task editors there are several classes on which to base your editors. You can start with [WorkflowTaskEditor](#class-workflowtaskeditor) or, if your workflow task derives from [ComponentTask](../classes/ComponentTask.md#class-componenttask), use [WorkflowComponentTaskEditor](#class-workflowcomponenttaskeditor). There are also some custom editors that are useful for editing the task properties:

*   [WorkflowValuesBindingEditor](#class-workflowvaluesbindingeditor)
*   [WorkflowCriteriaBuilder](#class-workflowcriteriabuilder)
*   [WorkflowDynamicValueItem](#class-workflowdynamicvalueitem)
*   [WorkflowTemplatedTextItem](#class-workflowtemplatedtextitem)

**Register Task Editor**

For the [Workflow Editor](#class-workfloweditor) to show your new task in the Add task choices and to edit existing tasks of your new type, a [WorkflowTaskDescriptor](#object-workflowtaskdescriptor) must be registered with Reify. easiest way to configure the descriptor is to add it to the default Reify task descriptors found in `[webroot]/tools/visualBuilder/workflowTasks.xml`.

As can be seen by looking at workflowTasks.xml, tasks are specified using a tree structure similar to that shown in the *tree XML loading example*. This tree structure exactly maps into the add task choices menu in the Workflow Editor. The properties that can be set on nodes are documented on [WorkflowTaskDescriptor](#object-workflowtaskdescriptor).

Alternately, a new task descriptor can be added by calling [Reify.registerWorkflowTaskDescriptor](#method-reifyregisterworkflowtaskdescriptor) which makes it possible to do this with ["Runtime Customization"](reifyOnSite.md#kb-topic-reify-onsite).

---
