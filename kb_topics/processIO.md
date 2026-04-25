# Process Input and Output Schema

[← Back to API Index](../reference.md)

---

## KB Topic: Process Input and Output Schema

### Description
A Process can declare optional schemas for what it consumes as input and what it produces as output on successful completion. These schemas let the engine validate wiring between a parent Process and a sub-Process invoked via [SubProcessTask](../classes/SubProcessTask.md#class-subprocesstask), and give subsystems like the Workflow Editor and AI tools a precise description of the Process's interface.

#### Input schema
Declared via [Process.inputDS](../classes/Process.md#attr-processinputds) (full [DataSource](../classes/DataSource_1.md#class-datasource)) or [Process.inputFields](../classes/Process.md#attr-processinputfields) (shorthand Array of [DataSourceField](../reference_2.md#object-datasourcefield) used to build a temporary DataSource). When a caller provides an input record (either at top-level via [Process.start](../classes/Process.md#method-processstart) or through a [SubProcessTask](../classes/SubProcessTask.md#class-subprocesstask)), the record is validated against the schema before the Process starts. On failure the Process does not start; the caller receives a [ProcessFailure](#type-processfailure) with `code:"inputValidation"`.

#### Output schema
Declared via [Process.outputDS](../classes/Process.md#attr-processoutputds) or [Process.outputFields](../classes/Process.md#attr-processoutputfields). When the Process reaches [handleFinished](#processhandlefinished) the engine computes the output value (see [Process.getOutput](../classes/Process.md#method-processgetoutput)) and validates it against the schema. A mismatch becomes a [ProcessFailure](#type-processfailure) with `code:"outputValidation"`.

#### Recoverable vs infrastructure errors
Recoverable errors that are part of the Process's normal behavior belong inside the declared `outputDS` (for example as nullable `errorCode`/`errorMessage` fields). Infrastructure failures (AI unavailable, JS exceptions, input/output schema mismatches, cancellation, ancestor-cycle deadlocks) travel through the distinct [Process.failed](../classes/Process.md#method-processfailed) channel as a [ProcessFailure](#type-processfailure) record.

---
