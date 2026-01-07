# Integrating AI Technology

[← Back to API Index](../reference.md)

---

## KB Topic: Integrating AI Technology

### Description
AI technology is woven into the SmartClient Framework, not only at a base level, but also systemically. With only minimal changes to application code, surprisingly sophisticated, AI-powered enhancements can be enabled that have the ability to turn the users of your application into power users. For example, users of your application can use natural language to:

*   Filter a [ListGrid](../classes/ListGrid_1.md#class-listgrid) according to their description of the records to include or exclude.
*   Add a custom field to a `ListGrid`, combining data from the underlying dataSource or augmenting the data with AI-provided knowledge.
*   Sort the data of a `ListGrid` according to the user's description of how the data should be ordered.
*   Build a custom [DataBoundComponent](../reference.md#interface-databoundcomponent) using available dataSources according to the user's description of what they would like to see.

#### The `AIEngine` class
Communication with AI services is performed by instances of the [AIEngine](../classes/AIEngine.md#class-aiengine) class. The following engines are built-in and don't require registration. Just put the appropriate API key in your [server configuration file](server_properties.md#kb-topic-serverproperties-file).

Note that this engine does not support vision requests.

| Engine ID | Provider | Name | Additional Installation Notes |
|---|---|---|---|
| "gpt-3.5-turbo" | OpenAI | GPT-3.5 Turbo | You must obtain an API key having access to the model(s) from: https://platform.openai.com/api-keysThen, the value of server configuration property OpenAI.api.key must be set to your API key.The o1-preview and o1-mini models may require higher tier API access. |
| "gpt-4" | OpenAI | GPT-4 |
| "gpt-4-turbo" | OpenAI | GPT-4 Turbo |
| "gpt-4o" | OpenAI | GPT-4o |
| "o1-preview" | OpenAI | o1-preview |
| "o1-mini" | OpenAI | o1-mini |
| "gemini-pro" | Google | Gemini Pro & Gemini Pro Vision | You must obtain an API key having access to these models from: https://makersuite.google.com/app/apikey?authuser=1Then, the value of server configuration property Gemini.api.key must be set to your API key. |

Note: The AI services corresponding to the IDs in AntiqueWhite do not support vision requests.

#### Enabling AI
AI is disabled by default. To enable AI within your application, just set [AI.defaultEngineId](../classes/AI.md#classattr-aidefaultengineid) to a different engine ID if you don't like the default, and then set [AI.disabled](../classes/AI.md#classattr-aidisabled) to `false`.

Here is sample SmartClient code that enables AI using GPT-4 Turbo:

```
 isc.AI.defaultEngineId = "gpt-4-turbo";
 isc.AI.disabled = false;
```
**Note:** If your application will need to ask AI to analyze images, you'll need an `AIEngine` that supports vision requests. Check the table above to see which built-in engines support vision, or you can register your own (covered below).
#### Adding your own AIEngine
If the built-in [AI Engines](../classes/AIEngine.md#class-aiengine) aren't enough, you can implement your own for the generative AI service that you would like to use, and [register](../classes/AI.md#classmethod-airegisterengine) it with the Framework. You can then set your engine's ID into [AI.defaultEngineId](../classes/AI.md#classattr-aidefaultengineid).

You can also [unregister](../classes/AI.md#classmethod-aiunregisterengine) an engine, or grab the `AIEngine` instance of a built-in or manually registered engine by passing the ID to [AI.getEngine](../classes/AI.md#classmethod-aigetengine).

#### AI Component Views and `AIServiceMode`
AI can be used to set up the view settings of a [ListGrid](../classes/ListGrid_1.md#class-listgrid), such as filters, sorts, and record hilites, according to the user's natural-language request for how the records should be filtered, sorted, and hilited. These AI-generated view settings are saved in the component [viewState](../reference.md#kb-topic-viewstate).

With each AI component view feature, there is an associated [AIServiceMode](../reference.md#type-aiservicemode) setting that controls the mode for how AI should respond to user requests:

| Filtering | [filterViaAIMode](../classes/ListGrid_1.md#attr-listgridfilterviaaimode) |
|---|---|
| Sorting | [sortViaAIMode](../classes/DataBoundComponent.md#attr-databoundcomponentsortviaaimode) |
| Hiliting | [hiliteViaAIMode](../classes/ListGrid_1.md#attr-listgridhiliteviaaimode) |

With respect to AI component views, the supported AI service modes are:

*   AI Assist - AI drives existing UI on the user's behalf according to the request. An example of this is: AI converts the user's description of what records they would like to see into [AdvancedCriteria](../reference.md#object-advancedcriteria) that is then set as the filter criterion of a `DataBoundComponent`.
*   AIDE (AI Data Enhance) - per-record augmentation or enhancements provided via AI. Examples of this are AI-generated fields, where the field values are not derived from the records, but rather, supplied via AI.
*   Hybrid - a combination of AI Assist and AIDE, where AI decides whether AI Assist, AIDE, or some combination of both approaches should be used to best respond to the request.

The amount of interaction with AI is lowest in AI Assist mode. AIDE requires more interaction with AI, and Hybrid mode requires the most amount of interaction. More interaction with AI generally requires more time to process the component view request.

#### Requirements for AI Component Views to be Enabled
With respect to a particular [DataBoundComponent](../reference.md#interface-databoundcomponent), the requirements for AI component views to be enabled are:

*   AI must be enabled: [AI.isEnabled](../classes/AI.md#classmethod-aiisenabled)
*   A globally-installed [DataSource](../classes/DataSource.md#class-datasource) with a primary key and [supporting AdvancedCriteria](../classes/DataSource.md#method-datasourcesupportsadvancedcriteria) must be set.
*   The `DataSource` cannot have a composite primary key.
*   The number of data-records must be known, and the total number of records must be less than the DBC's [aiMaxRecords](../classes/DataBoundComponent.md#attr-databoundcomponentaimaxrecords).

#### Best Practices for Integrating AI
SmartClient handles the process of assembling the context to AI automatically. There are, however, places where you can add application-specific context to improve AI's understanding of your application:

*   [DataSource.description](../classes/DataSource.md#attr-datasourcedescription) - An overview description of the data source.
*   [DataSource.sampleData](../classes/DataSource.md#attr-datasourcesampledata) - Example records that illustrate typical values, formats, and relationships in the data source.
*   [DataSourceField.description](../classes/DataSourceField.md#attr-datasourcefielddescription) - A description of a particular data source field.

See the linked APIs for guidance on the type of information to include in each attribute.

**Important:** Providing inaccurate or misleading information in these attributes can degrade AI performance and produce poor results.

---
