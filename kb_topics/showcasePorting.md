# Porting Showcase samples to React

[← Back to API Index](../reference.md)

---

## KB Topic: Porting Showcase samples to React

### Description
Converting a Showcase sample to a React app involves porting all of tabs in the sample that represent client-side code. There are several types of tabs to consider.
#### Main code tab
The main code tab is generally JavaScript, and often represents the complete sample, except for [DataSources](../classes/DataSource.md#class-datasource). You can port this code to a mixture of React JSX and JavaScript, following the rules described in the [reactIntegration](reactIntegration.md#kb-topic-integrating-pre-existing-smartclient-apps-with-react) help topic.

In a few cases, the main tab is [componentXML](componentXML.md#kb-topic-component-xml) to illustrate that format. Sometimes, you'll find the same sample is also present in the Showcase in JavaScript form. Component XML format is similar to SmartClient React JSX syntax, making porting straightfoward. For details of the differences between the formats, see the discussion at the bottom of the [reactIntegration](reactIntegration.md#kb-topic-integrating-pre-existing-smartclient-apps-with-react) help topic.

#### Extra code tabs
One or more additional code tabs may be present, typically widgets or data definitions in JavaScript, referenced by the main code. The sample was likely split into pieces just to make it easier to view and/or edit, so there's no requirement that your translated React app must preserve that separation. If you do decide to create separate files in your app for each sample tab, you'll need to assign a global ID to any widgets or data structures so they can be referenced cross-file.

If a tab declares an array of records, you may be better off just keeping that data as JS in your React app if the records contain non-string data, such as numbers or booleans, since SmartClient React JSX does not capture types. To convert such records to React JSX properly, you'd need to define a [client-only](../classes/DataSource.md#attr-datasourceclientonly) DataSource with those records as its [initial data](../classes/DataSource.md#attr-datasourcecachedata).

#### DataSource tabs
Another common tab in Showcase samples is a [DataSource](../classes/DataSource.md#class-datasource) definition. This will either be XML representing a server-based DataSource file or possibly JS representing a client-only DataSource.

If the tab contains the XML defining a server-based DataSource, it's just there for reference, and you don't need to port it as [SmartClient server technology](iscServer.md#kb-topic-smartclient-server-summary) can be used directly, unchanged, by your React app. You just need to make sure your app [loads the DataSource](dataSourceDeclaration.md#kb-topic-creating-datasources) before using it.

#### Comparison with Official React Showcase samples
In the Showcase, you can see React versions of several samples. You may see multiple tabs of React files, and in each there will be a call to `ReactDOM.render()`. This illustrates how you can target distinct DOM elements when inserting widgets hierarchies of SmartClient React JSX and allows the Showcase to load the tabs separately.

However, if you're porting a Showcase sample yourself, and want to split a widget hierarchy across files, it's suggested that you add an ID to the inner widget, and then reference it in the parent, which means that the DOM target passed to `ReactDOM.render()` for the inner widget will only be used to temporarily hold that widget before its attached to the parent.

### See Also

- [reactSupport](reactSupport.md#kb-topic-using-smartclient-with-react)

---
