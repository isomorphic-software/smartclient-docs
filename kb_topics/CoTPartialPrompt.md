# CoTPartialPrompt

[← Back to API Index](../reference.md)

---

## KB Topic: CoTPartialPrompt

### Description
Facilities for generating partial prompts with selected fragments omitted.

#### Purpose
When debugging CoT workflows, full prompts can be overwhelming—hundreds of kilobytes of UI summaries, DataSource schemas, action lists, and boilerplate obscure the specific logic being investigated. Partial prompts solve this by omitting irrelevant sections while preserving troubleshooting-relevant content.

#### Fragment Types
Prompts are composed of fragments that can be independently omitted:

*   **Built-in fragments:** goal, goalPrimer, history, historyPrimer, transitions, transitionsPrimer, errors, errorsPrimer, taskPrompt, introPrompt
*   **Process fragments:** entries from [CoTProcess.optionalPrompts](../classes/CoTProcess.md#attr-cotprocessoptionalprompts)
*   **State variables:** Any state.\* variable referenced in templates

#### Built-in Modes
Pre-configured modes target common troubleshooting scenarios. Pass a mode name to [CoTProcess.getPartialPrompt](../classes/CoTProcess.md#method-cotprocessgetpartialprompt):

*   **taskPromptOnly** - Debug task-specific prompt content
*   **transitionDebug** - Debug workflow transition logic
*   **stateTracking** - Track state variable changes
*   **historyOnly** - Focus on action history continuity
*   **errorsOnly** - Focus on validation/execution errors
*   **minimal** - Smallest useful prompt
*   **noData** - Omit large data, keep logic

Subclasses may define additional modes. Modes are resolved by looking for `this.promptMode[ModeName]` on the process instance.

#### Customizing Modes
Any mode can be customized via [PartialPromptConfig.add](../classes/PartialPromptConfig.md#attr-partialpromptconfigadd) and [PartialPromptConfig.remove](../classes/PartialPromptConfig.md#attr-partialpromptconfigremove): // Include history even though taskPromptOnly omits it process.getPartialPrompt({ mode: "taskPromptOnly", add: \["history"\] }); // Start with transitionDebug, also omit errors process.getPartialPrompt({ mode: "transitionDebug", remove: \["errors"\] });

### Related

- [CoTProcess.getPartialPrompt](../classes/CoTProcess.md#method-cotprocessgetpartialprompt)
- [AUN.getPartialPrompt](../classes/AUN.md#method-aungetpartialprompt)
- [AUN.exportMarkdownLog](../classes/AUN.md#method-aunexportmarkdownlog)
- [PartialPromptConfig](../reference.md#object-partialpromptconfig)
- [CoTProcess.promptModeTaskPromptOnly](../classes/CoTProcess.md#attr-cotprocesspromptmodetaskpromptonly)
- [CoTProcess.promptModeTransitionDebug](../classes/CoTProcess.md#attr-cotprocesspromptmodetransitiondebug)
- [CoTProcess.promptModeStateTracking](../classes/CoTProcess.md#attr-cotprocesspromptmodestatetracking)
- [CoTProcess.promptModeHistoryOnly](../classes/CoTProcess.md#attr-cotprocesspromptmodehistoryonly)
- [CoTProcess.promptModeErrorsOnly](../classes/CoTProcess.md#attr-cotprocesspromptmodeerrorsonly)
- [CoTProcess.promptModeMinimal](../classes/CoTProcess.md#attr-cotprocesspromptmodeminimal)
- [CoTProcess.promptModeNoData](../classes/CoTProcess.md#attr-cotprocesspromptmodenodata)
- [AUN.promptModeActionSelection](../classes/AUN.md#attr-aunpromptmodeactionselection)
- [AUN.promptModeUiScanDebug](../classes/AUN.md#attr-aunpromptmodeuiscandebug)
- [AUN.promptModeNavGraphDebug](../classes/AUN.md#attr-aunpromptmodenavgraphdebug)

### See Also

- [CoTProcess.getPartialPrompt](../classes/CoTProcess.md#method-cotprocessgetpartialprompt)
- [PartialPromptConfig](../reference.md#object-partialpromptconfig)

---
