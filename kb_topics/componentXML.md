# Component XML

[← Back to API Index](../main.md)

---

## KB Topic: Component XML

### Description
As covered in the _QuickStart Guide_ Chapter 4, _Coding_, SmartClient components can be created in either XML or JavaScript format. This section covers further details of using the XML format, called "SmartClient component XML".

**Referring to previously defined components**

To refer to another component by ID in XML, use `<Canvas withID=/>`. For example:

```
 <Canvas ID="myCanvas"/>
 <Canvas ID="myCanvas2"/>
 <VLayout>
     <members>
         <Canvas withID="myCanvas"/>
         <Canvas withID="myCanvas2"/>
     </members>
 </VLayout>
 
```

#### Loading screens stored in Component XML

Save your Component XML as a file called _screenName_.ui.xml under _webroot_/shared/ui/. Placing your .ui.xml file in this directory makes it visible to the system; the location of this directory can be configured in [server.properties](server_properties.md#kb-topic-serverproperties-file) by setting the _project.ui_ property. _screenName_ can be any valid identifier (no spaces, dashes or periods - underscores OK).

If you have multiple top-level tags (eg, your code is similar to the example above under "Referring to previousy defined components") use `<isomorphicXML>` as a top-level container tag - this has no impact on processing and is just an idiom to make your file valid XML, since XML does not allow multiple top-level tags in a document.

Component XML screens are then loaded using the ScreenLoaderServlet. The default SDK comes with this servlet already registered at _projectBase_/isomorphic/screenLoader . If you've modified web.xml or only included some of the default servlets, you may need to add it now - see the [Installation Instructions](iscInstall.md#kb-topic-installing-the-smartclient-runtime) .

To create an application that consists of _just_ the imported mockup, just add a `<script src>` tag pointing to the ScreenLoader servlet and referring to the _screenName_ you used when you saved your file. For example, if your application launches from a directory next to the "isomorphic" directory from the SDK:

```
    <script src="../isomorphic/screenLoader?screenName=screenName"></script>
 
```
If you want to load screens dynamically, or if you want to load more than one screen, use [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen). See the section on "Multiple screens and global IDs" below.

You can optionally enable "strict validation" for Component XML and DataSource files, which helps avoid typos, misspellings and other basic errors in your XML. See the [Strict Mode overview](strictMode.md#kb-topic-strict-mode) for details.

#### Embedding JavaScript code

To embed a JavaScript expression into component XML, use the `<JS>` tag. For example:

```
 <VLayout>
     <width><JS>isc.Page.getWidth() - 20</JS></width>
 </VLayout>
 
```
Note that, like all component XML properties, the `width` property can be specified either as an XML attribute or as a subelement. Expressing it as a subelement, as shown above, allows the `<JS>` tag to be used.

**Embedding Methods**

For [StringMethods](stringMethods.md#kb-topic-string-methods-overview) such as [ListGrid.recordClick](../classes/ListGrid_2.md#method-listgridrecordclick), JavaScript code can be used as an ordinary element value:

```
 <ListGrid>
     <recordClick>if (record.age > 65) doSomething()</recordClick>
 </ListGrid>
 
```
To embed an actual function definition, use the `<JS>` tag described above. For example:
```
 <ListGrid>
     <recordClick><JS>function (viewer, record, recordNum, field) {
          if (record.age > 65) doSomething();
     }</JS></recordClick>
 </ListGrid>
 
```
Unfortunately, characters commonly used in JavaScript code, such as ampersand (&), are not legal inside XML element or attribute values. For example, the expression "record != null && record.age > 65" must be written as shown below, or it is not considered valid XML:

```
 <ListGrid>
     <recordClick>
         if (record.status != null &amp;&amp; record.age > 65) doSomething()
     </recordClick>
 </ListGrid>
 
```
An alternative, for larger blocks of code, is to use the XML standard "CDATA" (character data) processing directive, which allows ampersand and other characters to be used without special notation:
```
 <ListGrid>
     <recordClick><![CDATA[
         if (record.status != null && record.age > 65) doSomething()
     ]]></recordClick>
 </ListGrid>
 
```

Overall, embedding code in XML can be awkward. Isomorphic generally recommends that significant chunks of JavaScript code, such as non-trivial custom components, be moved to separate, purely JavaScript files, while code embedded in component XML is limited to simple expressions and short functions. See the next section for details on keeping code in a separate file.

#### Event Handlers & Scripting loaded components

You can retrieve the components in your loaded screen in order to add event handlers to them, call APIs on them, place them into layouts you programmatically create, and in general add dynamic behavior. Retrieve the components via the [Canvas.getById](../classes/Canvas.md#classmethod-canvasgetbyid) API (note, when working with multiple screens, be sure to see the upcoming section about managing global IDs).

You can then add event handlers normally. For example, say there is a ListGrid with ID "mainGrid" and a DynamicForm with ID "editForm" in the same screen, and you want to populate the form with whatever record is clicked on in the grid:

```
   isc.Canvas.getById("mainGrid").addMethods({
       recordClick : "editForm.editRecord(record)"
   });
 
```

You can also add a loaded screen to an existing layout container. For example, perhaps you've already written parts of the application via normal coding techniques, and now you want to take a screen defined in Component XML and place it in a particular Layout you've already created ("existingLayout" below) - just use [Layout.addMember](../classes/Layout.md#method-layoutaddmember) as usual:

```
    existingLayout.addMember(isc.Canvas.getById("componentId"));
 
```
Component XML files can also refer to components you have created programmatically, and incorporate them into layouts. For example, if you have created a ListGrid component with ID "theGrid", you could refer to that grid using a ``<Canvas withID=""/>`` tag, which can be used anywhere a Canvas is expected. For example:
```
 <VLayout ... >
     <members>
           <Canvas withID="theGrid"/>
     </members>
 </VLayout>
 
```
Note that this approach requires that the referenced component has been created **before** `loadScreen` is called.

#### Declarative Actions

Component XML files can declare `Action`s to take in response to events. An `Action` is a declarative method call on this or some other component, with or without parameters. Being declarative, actions have some advantages over procedural code: they make your application easier to understand and easier to maintain, and they allow tools such as Reify to understand and edit your event handling logic.

To take a simple example, this is how you would declare an `Action` to display a record in a [DetailViewer](../classes/DetailViewer.md#class-detailviewer) when that record is clicked in a [ListGrid](../classes/ListGrid_1.md#class-listgrid).

```
   <ListGrid dataSource="Customer" autoID="customerGrid">
      ...
     <recordClick>
       <Action target="customerDetailViewer" name="viewSelectedData" mapping="viewer"/>
     </recordClick>
   </ListGrid>
 
```
The three elements of this declaration:

*   **target** is the global ID of the component on which the action will be called
*   **name** is the name of the method to call
*   **mapping** is an optional definition of the parameters to pass to the method. See the separate section on parameters below

`target` and `name` are both required attributes of any `Action`, and they must be valid. If `target` does not refer to a valid component, or `name` is not the name of a valid method on that component, you will generate a runtime error. Note, the rules around describing valid actions in the _**Declaring Events and Actions**_ section of the [componentSchema](componentSchema.md#kb-topic-component-schema) article apply to Reify only. When building applications through Reify, only methods marked `action="true"` will appear in the list of valid actions for a given target component. However, _any_ documented method can be called as an `Action` in manually-created Component XML, as can any registered [string method](stringMethods.md#kb-topic-string-methods-overview),

Event handlers can also invoke [workflow processes](../classes/Process.md#class-process), which are a special kind of multi-step `Action`. You specify a workflow process like this (see the [Process documentation](../classes/Process.md#class-process) for details of what goes inside the ``<Process>`` tag)

```
   <ListGrid dataSource="Customer" autoID="customerGrid">
      ...
     <recordClick>
       <Process>
          ...
       </Process>
     </recordClick>
   </ListGrid>
 
```

Finally, you are not limited to one `Action` per event: you can declare any number of `Action`s and/or `Process`es inside an event handler declaration.

#### Parameters and Actions

Parameters are defined in an `Action` declaration in the `mapping` attribute. This attribute is optional; if the target action method does not require parameters, this attribute can be omitted. If provided, `mapping` should be a comma-separated list of values. Each of these values is either:

*   A variable name
*   The special variable `this`, which is a reference to the source component (ie, the component upon which the `Action` is being defined)
*   A literal, like 'foo' or 17. Note, string literals must be enclosed in quotes, or they will be interpreted as variable names
*   A valid Javascript expression, like `new Date()`

Of these, the most interesting and most commonly-used are the first two. `Action`s are declared inside event handler declarations that correspond to SmartClient event methods. These methods are passed parameters, and these parameters are available, via the `mapping`, to any contained `Action`. Providing the correct mapping requires that you know the name of the parameter you are interested in, and this information is present in the documentation.

To take the above example, we want to call `viewSelectedData()` on the [DetailViewer](../classes/DetailViewer.md#class-detailviewer), so looking at the documentation for [DetailViewer.viewSelectedData](../classes/DetailViewer.md#method-detailviewerviewselecteddata), we can see that it takes a single parameter of type [ListGrid](../classes/ListGrid_1.md#class-listgrid) or [TileGrid](../classes/TileGrid.md#class-tilegrid), or the ID of a `ListGrid` or `TileGrid`. This parameter tells the `DetailViewer` which component's selected data to show, so we want to pass in the `ListGrid` itself, the component we are declaring this `Action` on.

One way to do this would be to use a mapping of `"this"`. As you can see from the example above, though, there is another way. If we look at the documentation for the event method wrapping our `Action` - [ListGrid.recordClick](../classes/ListGrid_2.md#method-listgridrecordclick) - we will see that it is passed a number of parameters, the first of which is a pointer to the `ListGrid` itself. As the documentation shows, this parameter is called "viewer". Therefore, we can use a `mapping` of "viewer". If we were declaring an `Action` to call a method that requires a [Record](../main.md#object-record) parameter, we can look at the documentation for `recordClick()` again and note that it is also passed the record just clicked, in a parameter called `record`. So our mapping for that `Action` would be "record".

#### Component XML and global IDs

A Component XML screen created in Reify or via the [Balsamiq importer](balsamiqImport.md#kb-topic-mockup-importer) will assign global IDs to all components generated from your mockup so that you can retrieve them by ID to add event handlers and call APIs. However if you build an application out of multiple screens built at different times, these IDs can collide, which will cause components to overwrite each other as they each try to use the same ID.

To solve this, the [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) API will _ignore_ global IDs on loaded components, assigning them sequential generated IDs instead (which will never collide). Instead of using global IDs, the callback for _loadScreen()_ will automatically provide you with the outermost component of a loaded screen, and that outermost component will provide access to other components by their original IDs via [Canvas.getByLocalId](../classes/Canvas.md#method-canvasgetbylocalid).

This allows you to add loaded screens to existing layouts, attach event handlers and take other programmatic actions, all without ever establishing global IDs.

#### Loading multiple screens

A typical application that uses screens stored in Component XML will have several such screens, or in some cases, hundreds or thousands. [RPCManager.cacheScreens](../classes/RPCManager.md#classmethod-rpcmanagercachescreens) can be used to load a set of screen definitions without actually creating any UI components - a subsequent call to [RPCManager.createScreen](../classes/RPCManager.md#classmethod-rpcmanagercreatescreen) is used to actually create the screen when needed. These two APIs provide the same global ID management facilities as [loadScreen()](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen).

As discussed in the [SmartClient Architecture overview](smartArchitecture.md#kb-topic-smartclient-architecture), screen definitions are typically very small, and should be loaded entirely up front or in very large batches. Further, screen _definitions_ have essentially negligible runtime overhead until the screen is actually created.

Therefore, use the following best practices for screen loading, even if you have very few or only one screen defined in Component XML:

*   at application startup, load all screens using [RPCManager.cacheScreens](../classes/RPCManager.md#classmethod-rpcmanagercachescreens)
*   create screens lazily (when they are about to be shown to the end user) using [RPCManager.createScreen](../classes/RPCManager.md#classmethod-rpcmanagercreatescreen).
*   for applications with very very large numbers of screens where loading all screen definitions up front creates a very large download, consider multiple calls to `cacheScreens()`, loading sets of screens that are likely to be used together.

#### Dynamic Component XML

Components can be dynamically provided on the server side by using the API defined in [`ScreenLoaderServlet.addDynamicScreenGenerator()`](http://www.smartclient.com/smartgwtee/server/javadoc/com/isomorphic/servlet/ScreenLoaderServlet.html#addDynamicScreenGenerator\(com.isomorphic.servlet.DynamicScreenGenerator\)) which allows adding DynamicScreenGenerators to the system for providing the .ui.xml files on the fly:

```
 ScreenLoaderServlet.addDynamicScreenGenerator(new DynamicScreenGenerator() {
      public String getScreen(String id) {

        if (id.equals("testDynamicScreenPrefix3")) {
            return null;
        }

        id=id.replace("testDynamicScreen","");
        return "";
      }
  }, "testDynamicScreenPrefix");
 
```

Whenever the system needs a screen in future, it will first call the registered DynamicScreenGenerator's `getScreen(String)` method for providing the given screen; Only if all queried DynamicScreenGenerators returns `null`, will proceed to use the normal system for obtaining the screen instances.

NOTE:

*   If this API is used, DynamicScreenGenerator will be called for **every** screen that the framework needs. Instead of this, the API contains alternative methods which will allow adding DynamicScreenGenerators only for a given string prefix or a regular expression.

In the provided example we register a DynamicScreenGenerator which will be called for each screen the system tries to load, if it starts with "testDynamicScreenPrefix", except the screen with id "testDynamicScreenPrefix3" for which we return null.

While registering a DynamicScreenGenerator is the first choice since is compatible with ScreenLoaderServlet's ability to load several screens in a single HTTPRequest, there are two additional ways to load Component XML screens - you can create a .jsp that uses the JSP tags that come with the SDK:

```
    <%@ taglib uri="http://www.smartclient.com/taglib" prefix="isomorphic" %>
    <isomorphic:XML>
       ... Component XML ...
    </isomorphic:XML>
 
```

Or you can use the server-side API com.isomorphic.XML.toJS():

```
     XML.toJS("<isomorphicXML xmlns:xsi=\"nativeType\">" +
                  componentXMLCode +                                 
                  "</isomorphicXML>");
 
```
However these two approaches will allow to only load one screen at a time. The JSP code above and the programmatic call to XML.toJS() both return a JavaScript code, which is the response that [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) expects. The `XML.toJS()` API can be easily combined with [direct use of the server-side DataSource API](standaloneDataSourceUsage.md#kb-topic-standalone-datasource-usage) to build a version of the ScreenLoaderServlet that can retrieve Component XML from a database or any Java API.

For static Component XML screens (cannot be changed at runtime), you can optionally run the XML.toJS() process as a build step to save a small amount of runtime overhead in XML to JS translation. Use [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) to load the resulting JavaScript by overriding the [RPCRequest.actionURL](../classes/RPCRequest.md#attr-rpcrequestactionurl) to point to the generated JavaScript file. Note that the overhead is minor enough that this is not worth doing unless you have a very large deployment and a very large number of static Component XML files.

#### Troubleshooting

XML parsing errors, which happen when XML is not well-formed and would be rejected by any standard XML parser, are reported in the server-side log, and, when possible, also in the client-side log within the "Results" tab of the Developer Console.

If you are loading a screen via the [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) API, you can see the response from the server in the RPC tab of the Developer Console - this will show you issues such as a misplaced ScreenLoaderServlet (HTTP response code will be 404 - Not Found) or responses that contain server exception details instead of the expected JavaScript response.

Other issues with component XML can result from incorrect use of SmartClient component XML tags. For example, you may specify a property and it may appear to have no effect even though it clearly works in other, JavaScript-based examples. If you get this symptom, you can troubleshoot by looking at the JavaScript code SmartClient generates from component XML.

You can also use the "Eval XML" section in the "Results" tab of the Developer Console to interactively experiment with Component XML ("Eval XML" button) and as a means of seeing the generated JavaScript ("Show JS" button).

#### Localization / Internationalization

Component XML files support embedding references to messages loaded from ResourceBundles via the same JSTL-like `<fmt>` syntax as is used for DataSource .ds.xml files. See [DataSource localization for details](dataSourceLocalization.md#kb-topic-datasource-and-component-xml-localization).

#### Custom Properties

If you specify a custom property on a component in XML, for example:

```
 <Canvas myProperty="false"/>
 
```
The value of the property will be a JavaScript String. In the above example, it would be the string "false", which is considered a boolean true value in the JavaScript language. If you want a different JavaScript type, you can force a property to be interpreted as a given type by using the "xsi:type" attribute:
```
 <Canvas>
     <myProperty xsi:type="xsd:boolean">false</myProperty>
 </Canvas>
 
```
The same notation works when you want to declare that an entire subobject has a given type. For example, this would cause the custom property "myListGrid" to have a live [ListGrid](../classes/ListGrid_1.md#class-listgrid) instance as it's value. All of the properties on the `<myListGrid>` tag will be correctly interpreted as ListGrid properties and have the correct types.
```
 <Canvas>
     <myListGrid xsi:type="ListGrid" width="500" height="600"/>
 </Canvas>
 
```
If you do not want an actual live ListGrid, but rather a JavaScript Object containing properties for later construction of a ListGrid, use the `propertiesOnly` attribute. For example, this code would cause the property "listGridProperties" to be a JavaScript Object with properties "width" and "height", whose values would be JavaScript Numbers.
```
 <Canvas>
     <listGridProperties xsi:type="ListGrid" propertiesOnly="true" 
                          width="500" height="600"/>
 </Canvas>
 
```
For your reference: "xsi" stands for "XML Schema Instance"; this notation derives from XML Schema standards for explicitly specifying type inline.

#### Custom Components

If you use [defineClass()](../classes/ClassFactory.md#classmethod-classfactorydefineclass) to define a new component class "MyListGrid" which is a subclass of the built-in component ListGrid, you can create it in XML as shown below:

```
 <ListGrid constructor="MyListGrid" width="500"/>
 
```
By using the `<ListGrid>` tag you advertise that properties should be interpreted as `ListGrid` properties. By specifying `constructor` you tell SmartClient what class to [create()](../classes/Class.md#classmethod-classcreate).

#### Component Schema

Instead of using the `constructor` and `xsi:type` attributes for custom components and custom properties, you can create a [componentSchema](componentSchema.md#kb-topic-component-schema) that describes the custom component. Declaring a component schema allows you to use your component just like the built-in SmartClient components, and also allows your component to be used within [Reify](reify.md#kb-topic-reify-overview).

---
