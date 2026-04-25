# DSRequestBuilderProcess Documentation

[← Back to API Index](../reference.md)

---

## Class: DSRequestBuilderProcess

*Inherits from:* [CoTProcess](CoTProcess.md#class-cotprocess)

### Description
A [CoTProcess](CoTProcess.md#class-cotprocess) that builds a [DSRequest](../reference_2.md#object-dsrequest) from a natural-language user prompt, governed by the JSON Schema produced by [DataSource.getDSRequestJSONSchema](DataSource_1.md#method-datasourcegetdsrequestjsonschema).

Intended as a shared building block invoked by other CoTs (AnswerEngine, ReportBuilder, and the ListGrid filter/sort/groupBy AI flows) whenever AI needs to emit a structured DSRequest. The calling code supplies the target DataSource and any related DataSources; the process sends an aiDialect-flavored schema to the AI, asks for a DSRequest matching that schema plus a brief reasoning string, and returns the DSRequest via its [output](#cotprocessoutput).

#### Inputs (populated via `process.state` before start)

*   `userPrompt` — the natural-language question.
*   `dataSourceID` — the target DataSource ID.
*   `relatedDataSourceIDs` — optional array of related DS IDs; used as [jSONSchemaSettings.relatedDataSources](#jsonschemasettingsrelateddatasources) on the generated schema so the AI can reference cross-DS paths via includeFrom / fieldQuery / valueQuery.

#### Outputs (on success)

*   `dsRequest` — the produced DSRequest object.
*   `reasoning` — one or two sentences from the AI describing its choices.

See [DataSource.getDSRequestJSONSchema](DataSource_1.md#method-datasourcegetdsrequestjsonschema) for the schema that governs the AI response and the full list of knobs that affect its shape.

---
## Attr: DSRequestBuilderProcess.outputFields

### Description
The two top-level keys the AI is asked to return (and that this process exposes on its output): `dsRequest` and `reasoning`.

**Flags**: IR

---
## Attr: DSRequestBuilderProcess.inputFields

### Description
Documents the shape of `process.state` the caller is expected to supply before starting the process.

**Flags**: IR

---
