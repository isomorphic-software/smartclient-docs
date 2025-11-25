# CoTExecutionModels

[← Back to API Index](../main.md)

---

## KB Topic: CoTExecutionModels

### Description
#### Execution Models: AIToolbox vs AIWorkflow
There are two primary ways to combine AI with external actions and application state. **AIToolbox** exposes a set of callable tools (functions/APIs) and lets the AI decide what to call, in what order, and when to stop; the orchestration lives inside the model. **AIWorkflow** declares an explicit workflow graph that the runtime executes externally, and the AI reasons within each step. AIWorkflow requires that state and history be tracked outside of the AI call itself so prompts can include the right context each time.
#### AIToolbox
The model receives tool definitions and self-orchestrates calls to them.

*   **Strengths:** fast to stand up; very flexible; minimal up-front design.
*   **Weaknesses:** non-deterministic sequencing; limited step-by-step monitoring; hard to audit; weak per-step testability since the model may choose different paths on each run; regressions are often detectable only at the final outcome layer.

#### AIWorkflow
The developer defines states and transitions in [CoTProcess](../classes/CoTProcess.md#class-cotprocess), each step implemented as a [CoTTask](../classes/CoTTask.md#class-cottask). The framework handles sequencing, validation, retries, state updates, and history; the AI focuses on reasoning inside each step. Because orchestration is external, behavior is consistent and observable.

*   **Strengths:** deterministic flow; per-step validation and retries; full observability (explicit state and history); easy auditing; highly testable—each task can be unit-tested in every workflow state; supports model specialization per task (e.g., a planner model for next-step choice, a codegen model for handlers).
*   **Trade-offs:** requires up-front workflow design; more structure than some quick experiments need.

#### Why AIWorkflow often suits enterprise
In enterprise contexts, AIWorkflow is typically more consistent, monitorable, predictable, auditable, and testable. It enables targeted prompt tuning and model comparisons at the task level, with regression tests that lock in improvements.

Specifically, with an AIWorkflow approach, you can test each individual task and tune the prompt until the AI does the task reliably, including switching which AI model is used for each task in the workflow: you might want a generalist model for decision tasks, but a coding-tuned model for codegen tasks.

In contrast, with the AIToolbox approach, you can only test the _overall result_ of the AI attempting the entire workflow, which is a much slower, compute-intensive, and ambiguous way of testing a given AI workflow, which also does not allow tuned models per step.

SmartClient supports both models, but we generally recommend AIWorkflow for enterprise tools where reliability and observability are critical, and AIToolbox for rapid prototyping or lightweight integrations where flexibility is more important than determinism.

Often, an AIToolbox approach is used for prototyping and then _evolves into_ and AIWorkflow approach, when determinism, testability, predictability and other factors become the key requirements of an actually deployed tool.

#### See also
\- [CoTProcess](../classes/CoTProcess.md#class-cotprocess) and [CoTTask](../classes/CoTTask.md#class-cottask) for the workflow APIs  
\- [CoT History](CoTHistory.md#kb-topic-cothistory) for how history is recorded and surfaced in prompts

---
