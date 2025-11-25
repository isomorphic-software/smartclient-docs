# Feature Explorer Overview

[← Back to API Index](../main.md)

---

## KB Topic: Feature Explorer Overview

### Description
The *Feature Explorer* is an example shell designed to help you explore the capabilities of SmartClient. Read on for a brief overview, including specific instructions for using the example code in your own standalone application.

The tree on the left of the Feature Explorer contains examples grouped by logical categories. Selecting an example brings it up on the right side of the screen, inside a tabbed view. The default "View" tab shows the interactive example itself, while other tabs show the underlying source. The "JS" tab shows the source for the example. There is sometimes also an "XML" tab that shows the corresponding version in [Component XML](componentXML.md#kb-topic-component-xml) format. For databound examples, there are also frequently additional tabs that show the [DataSources](../classes/DataSource.md#class-datasource) associated with the example.

**How to create a standalone application using code from the Feature Explorer**

The Feature Explorer shell is designed to show many examples in one place and to enable experimentation by providing a way for you to modify example code and try out your changes. As a result, the Feature Explorer requires some basic server support and its examples omit the usual SmartClient module includes that have to be in place for using SmartClient components standalone.

If you'd like to use example code in your application to get started quickly, create a page with SmartClient includes and then take the code from the "JS" tab and place it between `<SCRIPT>` blocks as described [here](nonJavaBackend.md#kb-topic-net-php-serverless-integration). If the example also includes a datasource, place the datasource definitions in the same file before the component code. Note that DataSources (and components) written in XML require the optional SmartClient server. If you're using the server, you can include them on your page using the [loadDSTag](loadDSTag.md#kb-topic-isomorphicloadds) tag.

**Feature Explorer difference in the LGPL package**

The LGPL edition of SmartClient does not include the SmartClient Java Server as part of the licensed software, but a trimmed down server is included in the package to support the Feature Explorer shell. There are some examples that use DataSources that would normally use the SmartClient server for persistence. In the LGPL package, these DataSources are automatically turned into [Client Only DataSources](clientOnlyDataSources.md#kb-topic-client-only-datasources) and the Feature Explorer loads the data for these one-time from the dataURL or testFileName attributes specified on the DataSource. Subsequent DataSource operations work against this client-side dataset, which is why changes to the data aren't permanent in these examples.

Check out the [Client-Server Integration](clientServerIntegration.md#kb-topic-client-server-integration) overview topic for an overview of your DataBinding options.

---
