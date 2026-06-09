# AI Assist

[← Back to API Index](../reference.md)

---

## KB Topic: AI Assist

### Description
AI Assist is the natural-language request layer of the SmartClient AI system. The user types (or dictates) a request, and a _delegator_ routes it to whichever registered _service_ is best suited to handle it. Applications plug in their own services to extend the system with app-specific behavior.

#### Three layers

*   **Entry points** — [AIAssistItem](../reference.md#class-aiassistitem) (a FormItem with an inline AI icon), [VoiceAssist](../classes/VoiceAssist.md#class-voiceassist) (dictation), or direct calls to [AI.delegate](../classes/AI.md#classmethod-aidelegate).
*   **Delegator** — [AIDelegator](../classes/AIDelegator.md#class-aidelegator), a lightweight [CoTProcess](../classes/CoTProcess.md#class-cotprocess) that asks the AI which registered service best matches the user's intent and then invokes it.
*   **Services** — pluggable units of work. Each [AIServiceDescriptor](#type-aiservicedescriptor) has a `name`, a natural-language `description`, and an `invoke(prompt, rationale, context)` function. Built-in services are `"answerEngine"` (data queries) and `"buildUI"` (create new UI from a natural-language description).

#### Flow
```
 user prompt → isc.AI.delegate(prompt, context, callback)
     |
     +-- 0 services: logWarn and return
     +-- 1 service:  invoke directly (skip AI)
     +-- 2+ services: AIDelegator CoTProcess asks AI "which service?"
                                 then invokes service.invoke(prompt, rationale, context)
 
```
#### Registering services
A service is just a [AIServiceDescriptor](#type-aiservicedescriptor) — an object with `name`, `description`, and `invoke`. The `description` is shown to the AI so it can decide whether this service is appropriate for a given request; keep it a concise sentence or two that names the class of requests this service handles and the class of requests it does _not_.

**Global services** are available regardless of which component has focus. Register them with [AI.registerAIService](../classes/AI.md#classmethod-airegisteraiservice):

```
 isc.AI.registerAIService({
     name: "lookupCustomer",
     description: "Looks up a customer by name, email, or phone and " +
         "opens their profile page.  Use for requests like 'find John " +
         "Smith' or 'open the profile for acme@example.com'.",
     invoke : function (userPrompt, rationale, context) {
         isc.AI.sendPrompt(userPrompt, {}, function (response) {
             // ...parse response, call application APIs...
         });
     }
 });
```

**Component-scoped services** are only available when the component (or one of its descendants) has focus. They let a specific screen, form, or widget add its own AI capabilities without affecting the rest of the application, and they shadow any global service of the same name. Register them with [Canvas.registerAIService](../classes/Canvas.md#method-canvasregisteraiservice):

```
 orderForm.registerAIService({
     name: "fillOrderForm",
     description: "Fills in this order entry form from a " +
         "natural-language description of the order.",
     invoke : function (userPrompt, rationale, context) {
         // context.focusCanvas is the form or a descendant
         orderForm.setValues(parseDescription(userPrompt));
     }
 });
```

#### Service discovery
When [AI.delegate](../classes/AI.md#classmethod-aidelegate) is called, it resolves the set of available services by walking the component hierarchy from `context.focusCanvas` upward, merging each ancestor's services with the global registry. Component-scoped services shadow global ones of the same name; nearest ancestor wins over farther. See [AI.getAIServicesForContext](../classes/AI.md#classmethod-aigetaiservicesforcontext).
#### Customizing the delegator
The prompts the [AIDelegator](../classes/AIDelegator.md#class-aidelegator) sends to the AI are fully customizable via [AI.delegatorPrompts](../classes/AI.md#classattr-aidelegatorprompts) — you can override the intro text, the primer before the service list, and the decision prompt itself. No code changes are required.
#### Invocation
[AI.delegate](../classes/AI.md#classmethod-aidelegate) is the primary entry point. It accepts the user's prompt, an optional context object (`{rootCanvas, focusCanvas}`), and an optional completion callback. Built-in UI — [AIAssistItem](../reference.md#class-aiassistitem) and [VoiceAssist](../classes/VoiceAssist.md#class-voiceassist) — route through it automatically; application code typically does not call it directly except when building its own entry points.
#### Error handling
If no services are registered, [AI.delegate](../classes/AI.md#classmethod-aidelegate) logs a warning and returns. If only one service is registered, it is invoked directly with no AI call. If the AI call fails (timeout, mock replay mismatch) or returns a service name that no longer matches any registered service, the first registered service is invoked as a fallback so the user's request is never silently dropped.

---
