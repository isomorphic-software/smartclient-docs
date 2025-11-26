# Adding Custom DataSources to Reify

[← Back to API Index](../reference.md)

---

## KB Topic: Adding Custom DataSources to Reify

### Description
DataSources placed in the project dataSources directory (\[webroot\]/shared/ds by default) will be detected by Reify whenever it is started, and appear in the DataSource listing in the lower right-hand corner automatically.

If you have created a custom subclass of DataSource (eg, as a base class for several DataSources that contact the same web service), you can use it with Reify by:

*   creating an XML version of the DataSource using the XML tag `<DataSource>` and the `constructor` property set to the name of your custom DataSource subclass (as described [componentXML](componentXML.md#kb-topic-component-xml) under the heading _Custom Components_)
*   modifying \[webroot\]/tools/visualBuilder/globalDependencies.xml to load the JavaScript code for your custom DataSource class. See examples in that file.

### See Also

- [toolsDeployment](toolsDeployment.md#kb-topic-tools-deployment)
- [reifyCustomComponents](reifyCustomComponents.md#kb-topic-adding-custom-components-to-reify)
- [reify](reify.md#kb-topic-reify-overview)

---
