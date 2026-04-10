# HumanTask Documentation

[← Back to API Index](../reference.md)

---

## Class: HumanTask

*Inherits from:* [Task](Task.md#class-task)

### Description
A server-side workflow task that requires human interaction to complete. When a HumanTask executes, the process suspends and task information is persisted to the [wfHumanTask](#attr-humantasktaskdatasource) DataSource for later completion.

**HumanTask vs UserTask**

[UserTask](UserTask.md#class-usertask) is designed for client-side workflows where a form is shown immediately to the current user. HumanTask is for server-side workflows where:

*   Tasks persist in a database for completion by any authorized user
*   A task inbox or console displays pending tasks
*   Tasks may be completed via API, email approval, or external system
*   Multiple UI presentation options are supported (Reify screens, external URLs)

**Data Flow**

HumanTask supports declarative input/output mapping similar to other workflow tasks:

*   [HumanTask.inputs](#attr-humantaskinputs): Selects data from process.state to pass to the task UI
*   [HumanTask.outputs](#attr-humantaskoutputs): Maps task completion data back to process.state

Task inputs are stored as [wfHumanTask.inputJSON](#wfhumantaskinputjson) when the task is created. When completed, user responses are stored as [wfHumanTask.outputJSON](#wfhumantaskoutputjson) and the [HumanTask.outputs](#attr-humantaskoutputs) mapping is applied to update process.state.

**UI Variants**

HumanTask supports multiple ways to present the task UI:

*   [HumanTask.externalURL](#attr-humantaskexternalurl): Opens external site in new window
*   [HumanTask.projectId](#attr-humantaskprojectid) + [HumanTask.screenId](#attr-humantaskscreenid): Loads Reify screen
*   [HumanTask.screenId](#attr-humantaskscreenid) alone: Loads standalone .ui.xml screen
*   [HumanTask.screenSource](#attr-humantaskscreensource): Creates screen from inline XML

When no UI variant is specified, a default completion form is shown based on [HumanTask.formFields](#attr-humantaskformfields).

### See Also

- [UserTask](UserTask.md#class-usertask)

---
## Attr: HumanTask.screenSource

### Description
JavaScript source code defining a screen to create via isc.createScreen(). This allows embedding simple task forms directly in the workflow definition.

Example:

```
 screenSource: '<DynamicForm ID="taskForm"><items>' +
               '<TextItem name="comments" title="Comments"/>' +
               '<CheckboxItem name="approved" title="Approved"/>' +
               '</items></DynamicForm>'
 
```

**Flags**: IR

---
## Attr: HumanTask.inputs

### Description
Specifies what data from process.state should be passed to the task UI. Supports the same formats as [Task.inputFieldList](Task.md#attr-taskinputfieldlist) and [CoTTask.inputs](Task.md#attr-taskinputs):

*   **Array**: List of state paths to copy, e.g. \["requestor", "amount"\]
*   **Object**: TaskInputExpression mapping, e.g. {approver: "$assignee"}
*   **String**: Single state path, e.g. "orderDetails"

The resolved input data is stored in [wfHumanTask.inputJSON](#wfhumantaskinputjson) when the task is created, and provided to the task screen via dataContext.

### Groups

- taskIO

### See Also

- [Task.inputFieldList](Task.md#attr-taskinputfieldlist)

**Flags**: IR

---
## Attr: HumanTask.windowTarget

### Description
Target for window.open() when using [HumanTask.externalURL](#attr-humantaskexternalurl). Common values:

*   "\_blank" - Opens in a new tab (default)
*   "\_self" - Opens in the same tab (not recommended)
*   A window name - Opens in a named window

**Flags**: IR

---
## Attr: HumanTask.dueDate

### Description
When this task should be completed by. Can be a dynamic expression like "$dueDate" to reference process state.

**Flags**: IR

---
## Attr: HumanTask.externalURL

### Description
External URL to open for this task. When specified, the user is sent to this URL in a new browser tab or window. Use [HumanTask.windowTarget](#attr-humantaskwindowtarget) and [HumanTask.windowFeatures](#attr-humantaskwindowfeatures) to control how the window opens.

When using externalURL, the workflow cannot automatically detect when the user has completed the external task. The task must be completed manually via the workflow console or API.

**Flags**: IR

---
## Attr: HumanTask.outputSchemaId

### Description
DataSource ID used to validate task output data. If specified, the user's form submission is validated against this schema before being accepted.

**Flags**: IR

---
## Attr: HumanTask.taskDescription

### Description
Description of what needs to be done to complete this task.

**Flags**: IR

---
## Attr: HumanTask.reifyServerURL

### Description
URL of a remote Reify server from which to load the task screen. Used together with [HumanTask.projectId](#attr-humantaskprojectid) and [HumanTask.screenId](#attr-humantaskscreenid).

If not specified but projectId and screenId are set, the current server is assumed to be a Reify server.

**Flags**: IR

---
## Attr: HumanTask.taskDataSource

### Description
DataSource to use for persisting task information.

**Flags**: IR

---
## Attr: HumanTask.priority

### Description
Priority of this task (higher numbers = higher priority).

**Flags**: IR

---
## Attr: HumanTask.candidateUsers

### Description
Users that can claim and complete this task.

**Flags**: IR

---
## Attr: HumanTask.candidateGroups

### Description
Groups that can claim and complete this task.

**Flags**: IR

---
## Attr: HumanTask.assignee

### Description
User ID of the person assigned to complete this task. Can be a dynamic expression like "$userId" to reference process state.

**Flags**: IR

---
## Attr: HumanTask.persistTask

### Description
Whether to persist task info to the wfHumanTask DataSource. When true, task details are saved for external systems to query.

**Flags**: IR

---
## Attr: HumanTask.waitDataSource

### Description
DataSource to use for persisting wait records.

**Flags**: IR

---
## Attr: HumanTask.windowFeatures

### Description
Features string for window.open() when using [HumanTask.externalURL](#attr-humantaskexternalurl). Controls window size, position, and chrome. Example: "width=800,height=600,menubar=no,toolbar=no"

If null, the browser's default behavior is used (typically a new tab).

**Flags**: IR

---
## Attr: HumanTask.taskName

### Description
Human-readable name for this task, displayed in task lists.

**Flags**: IR

---
## Attr: HumanTask.projectId

### Description
Reify project ID containing the screen to display for this task. Used together with [HumanTask.screenId](#attr-humantaskscreenid), and optionally [HumanTask.reifyServerURL](#attr-humantaskreifyserverurl).

**Flags**: IR

---
## Attr: HumanTask.screenId

### Description
Screen ID to display for this task. Can be used in several ways:

*   With [HumanTask.projectId](#attr-humantaskprojectid): loads screen from a Reify project
*   Alone: loads standalone screen via [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen)

**Flags**: IR

---
## Attr: HumanTask.outputs

### Description
Specifies how task completion data should be mapped back to process.state. Uses the same StateUpdates format as [CoTTask.stateUpdates](CoTTask.md#attr-cottaskstateupdates):
```
 outputs: {
     "approval.decision": "$decision",
     "approval.comments": "$comments",
     "approval.timestamp": "$currentTime"
 }
 
```
Keys are state paths (destination), values are TaskInputExpressions that reference the completed form values. When the task is completed, these mappings are applied via [Process.applyStateUpdates](Process.md#method-processapplystateupdates).

If outputs is not specified, [Task.outputFieldList](Task.md#attr-taskoutputfieldlist) or [Task.outputField](Task.md#attr-taskoutputfield) are used instead.

### Groups

- taskIO

### See Also

- [Task.outputFieldList](Task.md#attr-taskoutputfieldlist)
- [CoTTask.stateUpdates](CoTTask.md#attr-cottaskstateupdates)

**Flags**: IR

---
## Attr: HumanTask.inputSchemaId

### Description
DataSource ID used to validate task input data. If specified, the input record built from [HumanTask.inputs](#attr-humantaskinputs) is validated against this schema before being stored.

**Flags**: IR

---
## Attr: HumanTask.formFields

### Description
Fields that the user should fill in when completing this task. These define the expected output structure.

**Flags**: IR

---
## ClassMethod: HumanTask.completeTask

### Description
Completes a pending human task and resumes the associated workflow. This is called when a user completes the task through an external system.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskId | [String](#type-string) | false | — | ID of the task to complete |
| taskOutput | [Object](../reference.md#type-object) | false | — | Output data from the completed task |
| completedBy | [String](#type-string) | true | — | User ID of the person completing the task |
| callback | [Callback](../reference.md#type-callback) | true | — | Called with (success, taskRecord) after completion |

---
## ClassMethod: HumanTask.claimTask

### Description
Claims a pending human task for a specific user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| taskId | [String](#type-string) | false | — | ID of the task to claim |
| userId | [String](#type-string) | false | — | User ID claiming the task |
| callback | [Callback](../reference.md#type-callback) | true | — | Called with (success, taskRecord) |

---
