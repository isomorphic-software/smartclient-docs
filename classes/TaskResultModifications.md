# TaskResultModifications Documentation

[← Back to API Index](../reference.md)

---

## Attr: TaskResultModifications.errors

### Description
Validation errors to attach to the current Task, in the standard format used by [DSResponse.errors](DSResponse.md#attr-dsresponseerrors): an Object where each property name is a field name of the Task's outputs and each value is the error information for that field.

Returning `errors` rejects the outputs: nothing is committed to [state](Process.md#attr-processstate) and the process does not advance. For a [CoTTask](CoTTask.md#class-cottask), the errors are automatically fed back to the AI in the next prompt (introduced by the [errorsPrimer](CoTTask.md#attr-cottaskerrorsprimer)) and the task is retried, up to [CoTTask.maxRetries](CoTTask.md#attr-cottaskmaxretries), so there is normally nothing further to do. See [AIRetriesExhausted](../kb_topics/AIRetriesExhausted.md#kb-topic-airetriesexhausted) for what happens when retries run out.

**Flags**: IR

---
## Attr: TaskResultModifications.stateUpdates

### Description
Additional declarative updates to apply to [state](Process.md#attr-processstate) before routing. Keys use [StatePath](../reference_2.md#type-statepath) semantics.

**Flags**: IR

---
## Attr: TaskResultModifications.outputs

### Description
Optional replacement for the Task's outputs. If provided, this replaces the outputs produced by the Task for the purposes of subsequent validation, state updates, history, and routing.

**Flags**: IR

---
