# CoTTask Documentation

[← Back to API Index](../reference.md)

---

## Class: CoTTask

### Description
Performs a call to an AI (LLM) and processes the results.

Provides declarative support for prompt assembly, AI-driven transitions to other states, validation & retries, storage of AI-generated results, and other features designed to make definitions of Chain-of-Thought (CoT) AI workflows as simple & declarative as possible.

Overview:

1.  assembles a prompt, typically in collaboration with a CoTProcess, such that only [taskPrompt](#taskprompt) is set on the task; this includes automatic prompt generation regarding [transitions](#transitions), [CoTProcess.history](#attr-cotprocesshistory) and [validation errors](#outputds) in the event of a retry
2.  contacts the configured LLM, which can be [AI.defaultAIEngineId](#aidefaultaiengineid) or can be specified as [task.aiEngineId](#attr-cottaskaiengineid) or [process.aiEngineId](#attr-cotprocessaiengineid)
3.  processes the AI response, in particular executing AI-driven [transitions](#transitions) to other states, applying [validation](#outputfields), and [auto-retrying](#maxretries) if validation fails
4.  for a successful response, can declaratively store results ([stateUpdates](#stateupdates)) and can invoke custom processing ([processOutputs](#method-processoutputs))
5.  after success, transitions using standard [Task](Task.md#class-task) semantics (nextElement or sequence), with a special fallback of returning to the calling task or to [CoTProcess.defaultReturnTask](#attr-cotprocessdefaultreturntask) if configured

### Groups

- CoT

---
