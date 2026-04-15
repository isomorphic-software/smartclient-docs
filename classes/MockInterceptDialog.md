# MockInterceptDialog Documentation

[← Back to API Index](../reference.md)

---

## Class: MockInterceptDialog

*Inherits from:* [Window](Window.md#class-window)

### Description
Base class for AI mock intercept dialogs. Provides common chrome including a collapsible prompt viewer, status area, and action buttons. Subclasses provide the response editor appropriate to their abstraction level.

This class is not typically instantiated directly. Instead, use:

*   [AIInterceptDialog](../reference.md#class-aiinterceptdialog) for raw AI request interception
*   [CoTInterceptDialog](CoTInterceptDialog.md#class-cotinterceptdialog) for CoT workflow task interception

### Groups

- AIMocking

---
## Attr: MockInterceptDialog.responseCallback

### Description
Callback fired when the user makes a choice.

Signature: `callback(response, action)` where:

*   `response` - The response object (null for skip/cancel)
*   `action` - One of "use", "skip", or "cancel"

**Flags**: IR

---
## Attr: MockInterceptDialog.prompt

### Description
The prompt text to display in the collapsible prompt viewer.

**Flags**: IR

---
## Attr: MockInterceptDialog.mockEntry

### Description
Pre-existing mock data to populate the response editor with.

**Flags**: IR

---
## Attr: MockInterceptDialog.showSkipButton

### Description
Whether to show the "Skip" button. Defaults to true for CoT-level dialogs where skipping a task makes sense. Set to false for AI-level dialogs where there is no meaningful "skip" semantic.

**Flags**: IR

---
## Method: MockInterceptDialog.createResponseEditor

### Description
Creates and returns the response editor component. Subclasses override to provide an appropriate editor (TextArea for raw, DynamicForm for structured).

### Returns

`[Canvas](#type-canvas)` — The response editor component

---
## Method: MockInterceptDialog.populateEditorFromResponse

### Description
Populates the editor with a response object (from mockEntry or AI response).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [Object](../reference.md#type-object) | false | — | The response data to populate |

---
## Method: MockInterceptDialog.getHeaderContents

### Description
Returns HTML for the header section. Subclasses override to show level-specific context (task ID, engine name, etc.).

### Returns

`[String](#type-string)` — HTML content for header

---
## Method: MockInterceptDialog.sendToAI

### Description
Sends the prompt to the real AI service. Subclasses override to use appropriate AI calling mechanisms for their level.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | Called with (response, error) when complete |

---
## Method: MockInterceptDialog.getResponseFromEditor

### Description
Extracts the response value from the editor. Returns null if validation fails (subclass should show an error message in this case).

### Returns

`[Object](../reference.md#type-object)` — The response object, or null if invalid

---
