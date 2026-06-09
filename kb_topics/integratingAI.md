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
Communication with AI services is performed by instances of the [AIEngine](../classes/AIEngine.md#class-aiengine) class. Several engines are built-in and don't require registration. Call [AI.getSupportedEngineIds](../classes/AI.md#classmethod-aigetsupportedengineids) to retrieve the current list of built-in engine IDs at runtime, or [AI.getSupportedEngineData](../classes/AI.md#classmethod-aigetsupportedenginedata) for full engine configuration including each engine's `apiKeyProperty`.

Each provider requires a developer API key - not the login credentials or OAuth token associated with a paid consumer account such as ChatGPT Plus or Claude Pro. Consult your provider's developer documentation to obtain a separate API key, then set it in your [server configuration file](server_properties.md#kb-topic-serverproperties-file) using the property name given by the `apiKeyProperty` field returned by [AI.getSupportedEngineData](../classes/AI.md#classmethod-aigetsupportedenginedata).

Note that some built-in engines do not support vision requests. Call [AIEngine.canSupportVisionRequests](../classes/AIEngine.md#method-aienginecansupportvisionrequests) on a retrieved engine instance to check.

#### Enabling AI
AI is disabled by default. To enable AI within your application, just set [AI.defaultEngineId](../classes/AI.md#classattr-aidefaultengineid) to a different engine ID if you don't like the default, and then set [AI.disabled](../classes/AI.md#classattr-aidisabled) to `false`.

Here is sample SmartClient code that enables AI using GPT-4.1:

```
 isc.AI.defaultEngineId = "gpt-4.1";
 isc.AI.disabled = false;
```
**Note:** If your application will need to ask AI to analyze images, you'll need an `AIEngine` that supports vision requests. Call [AIEngine.canSupportVisionRequests](../classes/AIEngine.md#method-aienginecansupportvisionrequests) on a retrieved engine instance to check, or you can register your own engine (covered below).
#### AWS Bedrock
Amazon Bedrock is not a model in itself but a managed service that provides access to multiple foundation models through a single AWS API. Instead of interacting directly with a specific AI vendor (as you would with OpenAI, Anthropic or Gemini), you connect to Bedrock and select which underlying model to use; Bedrock supports many such models, including Mistral, Meta Llama, Amazon's own Titan and Nova engines, Deepseek, and others (including OpenAI GPT and Anthropic Claude, which you can also connect to directly).

Therefore, Bedrock is an intermediary layer rather than the actual model provider. The most important thing about Bedrock integration into SmartClient is that it gives you access to a wide selection of models from numerous different AI providers, without the need for native support for all those different providers. It also means that billing is done through your AWS account rather than directly with the company that is providing the underlying AI service.

Bedrock integration requies a couple of additional `server.properties` entries, in addition to the API key:

*   `**Bedrock.api.aws.region**` Like other AWS services, Bedrock is a regional service, so we must connect to the endpoint of the region where you want the inference to run. Provide a valid AWS region in this property - for example `us-east-2` or `eu-central-1`
*   `**Bedrock.api.model**` As mentioned above, Bedrock itself is not an AI model, so you must provide the name of the model to use. This must be a valid modelId or ARN that you have access to through the AWS account associated with your API key. This is not a completely straightforward topic and you should consult AWS Bedrock documentation to work out the correct modelId or ARN to specify

#### Adding your own AIEngine
If the built-in [AI Engines](../classes/AIEngine.md#class-aiengine) aren't enough, even with Bedrock support, you can implement your own for the generative AI service that you would like to use, and [register](../classes/AI.md#classmethod-airegisterengine) it with the Framework. You can then set your engine's ID into [AI.defaultEngineId](../classes/AI.md#classattr-aidefaultengineid).

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
*   A globally-installed [DataSource](../classes/DataSource_1.md#class-datasource) with a primary key and [supporting AdvancedCriteria](../classes/DataSource_2.md#method-datasourcesupportsadvancedcriteria) must be set.
*   The `DataSource` cannot have a composite primary key.
*   The number of data-records must be known, and the total number of records must be less than the DBC's [aiMaxRecords](../classes/DataBoundComponent.md#attr-databoundcomponentaimaxrecords).

#### Best Practices for Integrating AI
SmartClient handles the process of assembling the context to AI automatically. There are, however, places where you can add application-specific context to improve AI's understanding of your application:

*   [DataSource.description](../classes/DataSource_1.md#attr-datasourcedescription) - An overview description of the data source.
*   [DataSource.sampleData](../classes/DataSource_1.md#attr-datasourcesampledata) - Example records that illustrate typical values, formats, and relationships in the data source.
*   [DataSourceField.description](../classes/DataSourceField.md#attr-datasourcefielddescription) - A description of a particular data source field.

See the linked APIs for guidance on the type of information to include in each attribute.

**Important:** Providing inaccurate or misleading information in these attributes can degrade AI performance and produce poor results.

---
