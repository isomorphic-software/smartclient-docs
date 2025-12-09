# PartialPromptConfig Documentation

[← Back to API Index](../reference.md)

---

## Attr: PartialPromptConfig.omitStateVars

### Description
State variable names to omit from prompt templates.

When a template contains `${state.varName}`, the reference will be replaced with a placeholder like `[state.varName omitted]`.

Specify variable names without the "state." prefix, e.g., `["eventStream", "currentSummary"]` to omit `${state.eventStream}` and `${state.currentSummary}`.

**Flags**: IR

---
## Attr: PartialPromptConfig.mode

### Description
Name of a built-in mode to use as the base configuration.

The mode is resolved by looking for `this.promptMode[ModeName]` on the process instance. For example, `mode: "taskPromptOnly"` looks for `this.promptModeTaskPromptOnly`.

Available built-in modes on CoTProcess:

*   **taskPromptOnly** - Focus on task-specific prompt; omit shared boilerplate
*   **transitionDebug** - Keep transitions visible; omit intro and history
*   **stateTracking** - Keep state variables and history; omit boilerplate
*   **historyOnly** - Focus on action history
*   **errorsOnly** - Focus on validation errors
*   **minimal** - Smallest useful prompt (goal + taskPrompt only)
*   **noData** - Omit large data but keep logic; truncate history/errors

### See Also

- [PartialPromptConfig.add](#attr-partialpromptconfigadd)
- [PartialPromptConfig.remove](#attr-partialpromptconfigremove)

**Flags**: IR

---
## Attr: PartialPromptConfig.add

### Description
Fragments to include even if the base mode would omit them.

Used when customizing a built-in mode to restore specific fragments. The names can be fragment names or state variable names (to restore from omitStateVars).

### See Also

- [PartialPromptConfig.remove](#attr-partialpromptconfigremove)

**Flags**: IR

---
## Attr: PartialPromptConfig.omit

### Description
Fragment names to omit from the prompt. Valid built-in fragment names:

*   `"introPrompt"` - process-level intro boilerplate
*   `"goal"` - goal primer and goal text
*   `"goalPrimer"` - just the goal primer (keep goal text)
*   `"history"` - history primer and all entries
*   `"historyPrimer"` - just the history primer (keep entries)
*   `"transitions"` - transition primer and definitions
*   `"transitionsPrimer"` - just the transition primer
*   `"errors"` - error primer and validation errors
*   `"errorsPrimer"` - just the error primer
*   `"taskPrompt"` - task-specific prompt content

Also supports any key from [CoTProcess.optionalPrompts](CoTProcess.md#attr-cotprocessoptionalprompts).

**Flags**: IR

---
## Attr: PartialPromptConfig.truncateHistory

### Description
Maximum number of history entries to include (most recent).

When set, only the last N history entries are included; earlier entries are replaced with a count indicator like "\[N earlier entries omitted\]".

**Flags**: IR

---
## Attr: PartialPromptConfig.remove

### Description
Additional fragments to omit beyond what the base mode specifies.

Used when customizing a built-in mode to omit additional fragments. The names can be fragment names (added to omit) or state variable names (added to omitStateVars).

### See Also

- [PartialPromptConfig.add](#attr-partialpromptconfigadd)

**Flags**: IR

---
## Attr: PartialPromptConfig.truncateErrors

### Description
Maximum number of error messages to include.

When set, only the first N error messages are included; remaining errors are replaced with a count indicator like "\[N more errors omitted\]".

**Flags**: IR

---
