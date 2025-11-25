# Using SmartClient with React

[← Back to API Index](../main.md)

---

## KB Topic: Using SmartClient with React

### Description
SmartClient has robust & comprehensive support for React, including full support for JSX and the complete SmartClient API, hundreds of samples, and full support for our low code platform, Reify.

All SmartClient components are available in React by importing our [npm module](npmjs.md#kb-topic-npmjs-support). React JSX can be used to create and configure SmartClient components, including things like ListGrids and their field definitions. The JSX syntax we support is essentially the same as our existing Component XML standard, with minor differences that are explained below. For post-render changes, such as hiding or showing a ListGrid field, the full SmartClient API is available in React via the standard "ref" mechanism - the same approach used in other popular React frameworks like agGrid, Sencha and Kendo (examples are below).

In the SmartClient Showcase, you can click on the React and see hundreds of samples - the same sample set we offer for SmartClient usage in normal JavaScript. Reify screens can be loaded into a React app with a single method call (Reify.loadProject()), or, since Reify screens are Component XML, screens created in Reify can be integrated as JSX. As with SmartClient in general, you can use the SmartClient Java Server, or any other server technology (via REST and various other built-in integration strategies).

#### Installing SmartClient support for React

To install support for SmartClient Eval, SmartClient LGPL, or another licensed SmartClient product for your React app, go to your app's root directory, and then follow the instructions for [installing SmartClient with npm](npmjs.md#kb-topic-npmjs-support). This will place the SmartClient framework under `isomorphic/` in your project's root directory, and install the SmartClient React support under `isomorphic/` in your project's source directory. So from your project's root directory, you might invoke the command line:

```
 npm install smartclient-eval --branch=13.1
```

#### React JSX and differences from Component XML

React JSX (shown in blue) can be used to declare SmartClient components as in this sample file:

```
 import React from 'react';
 import 'smartclient-eval/release';
 import 'smartclient-eval/skins/Tahoe';
 import { SC, IButton } from 'smartclient-eval/react';

 SC.render(
     <DynamicForm numCols="3" autoFocus="true">
         <items>
             <TextItem defaultValue="my friend" name="you" title="Enter your name"
                       wrapTitle="false" selectOnFocus="true"/>
             <ButtonItem icon="[SAMPLE]icons/16/message.png" title="Hello" width="80"
                         startRow="false" click={onButtonItemClick}/>
         </items>
     </DynamicForm>,
     document.getElementById("app")
 );
```
where the SmartClient utility class `SC` provides a `render()` method that internally calls `ReactDOM.render()` in React pre-18, and `ReactDOM.createRoot().render()` in React 18+, so we don't need different code per React version, yet still avoid deprecation warnings.

With a few exceptions, you should be able to use [Component XML](componentXML.md#kb-topic-component-xml) syntax to specify widgets and objects in JSX:

*   [Canvas.children](../classes/Canvas.md#attr-canvaschildren) should be specified in JSX with the tag `childComponents` instead, since React reserves the use of the `children` property.
*   [ListGridFIelds](../main_2.md#object-listgridfield) should be declared in JSX via the tag `LGField` rather than `field` as in Component XML, since in React types are expected to be capitalized and clearly denote the underlying object type. The same applies to [DataSources](../classes/DataSource.md#class-datasource) and other [DBCs](../main.md#interface-databoundcomponent), such as [TreeGrids](../classes/TreeGrid.md#class-treegrid), [TileGrids](../classes/TileGrid.md#class-tilegrid) and [DetailViewers](../classes/DetailViewer.md#class-detailviewer), where respectively the tags to use are `DSField`, `TGField`, and then `DVField` (for both TileGrid and DetailViewer fields).
    
    For example:
    
    ```
     <ListGrid ID="myGrid" width="100%">
         <fields>
             <LGField name="countryName" title="Country Name" width="200"/>
             <LGField name="population"  title="Population" type="integer"/>
             <LGField name="area"        title="Land Area" type="integer"/>
         </fields>
     </ListGrid>
    ```
    
*   [FormItems](../classes/FormItem.md#class-formitem) in a [DynamicForm](../classes/DynamicForm.md#class-dynamicform) should be specified with the actual tag name of the form item class, such as `TextItem` or `ButtonItem`.
*   While string methods can be specified in both JSX and Component XML by just assigning the string to an attribute, JSX does not support Component XML's `JS` tag for declaring a JavaScript method inside an element. Instead, you should assign methods by using the inline JS syntax for JSX that assigns JavaScript directly to attributes:
    ```
     let myHover = function () {
         return "Hello on " + new Date();
     }
     SC.render(
         <Canvas border="2px solid red" backgroundColor="yellow" canHover="true" getHoverHTML={myHover}/>,
         document.getElementById("app")
     );
    ```
    
*   [ValueMaps](../main_2.md#type-valuemap) or other JS objects that have capitalized property names, or property names that aren't valid [Identifiers](../main.md#type-identifier) will not parse as React JSX. So the following Component XML, for example, declared as the value of the `valueMap` property for a component, is _not_ valid JSX:
    ```
     <valueMap>
         <Weather>Current Weather</Weather>
         <Year>Expedition Year</Year>
     </valueMap>
    ```
    You must instead inline the values as attributes:
    ```
     <valueMap Weather="Current Weather" Year="Expedition Year"/>
    ```
    or you can switch to lowercased ValueMap value tags. This also applies to generic JS objects you're assigning as component properties, if they have capitalized property names.
    
    If the ValueMap tag names aren't even valid identifiers, inlining as above won't work, but you can use the alternate ValueMap syntax. So for example:
    
    ```
     <SelectItem name="level">
         <valueMap>
             <value ID="1">debug</value>
             <value ID="2">notify</value>
             <value ID="3">warning</value>
             <value ID="4">error</value>
        </valueMap>
     </SelectItem>
    ```
    In all of these cases, you also have the option of just moving the ValueMap or JS object definition up before the JSX and declaring it as JS, and then inlining it by reference as was shown earlier for functions.
*   React JSX doesn't support redeclaring components defined earlier by applying the `withID` attribute like Component XML. If you need to refer to other components, such as for example with the [Layout.minBreadthMember](../classes/Layout.md#attr-layoutminbreadthmember) property, you should just refer to them by global ID, where the Framework supports it. You can also refer to components directly via the inline JS syntax for JSX, but only for components defined before the current JSX hierarchy, as JS inlining is applied to the entire hierarchy before any of components in it are created.

Your component's definition can be split between JS and JSX, with most of the configuration remaining in JS if you prefer. For example:
```
 let fields = [{
     name: "countryName", title: "Country Name", width: 150
 }, {
     name: "population", title: "Population", type: "integer"
 }, {
     name: "area", title: "Land Area", type: "integer"
 }];
 let gridConfig = {
     width: 400, height: 200,
     canEdit: true, autoFitFieldWidths: true,
     initialCriteria: {countryName: "United States"}
 };
 SC.render(
    <ListGrid ID="countryGrid" fields={fields} {...gridConfig} />,
    document.getElementById("app")
 );
```
Here, the ListGridFields have been defined in JavaScript, and applied using the inline JS syntax for JSX, while the rest of the grid's configuration has been applied using the JavaScript ES6 spread operator. The spread operator allows you to merge JS config with JSX attributes while declaring a SmartClient React component.

#### Component lifecycle

SmartClient React support works with the standard [React lifecycle](https://medium.com/codex/the-lifecycle-of-a-react-component-8e01332a068d) and provides helper methods on a component if you need to have access to them. The available functions are:

*   beforeRender()
*   beforeComponentDidMount()
*   afterComponentDidMount()
*   beforeComponentDidUpdate()
*   afterComponentDidUpdate()
*   beforeComponentWillUnmount()
*   afterComponentWillUnmount()

For example:
```
 import React from 'react';
 import ReactDOM from 'react-dom';
 
 import 'smartclient-eval/release';
 import 'smartclient-eval/skins/Tahoe';
 
 import { Button } from 'smartclient-eval/react';
 
 let beforeComponentDidMount = function() {
     console.log('Will be executed before componentDidMount step');
 };
 
 ReactDOM.render(
     <Button title="Hello, world" width="150" 
         beforeComponentDidMount={beforeComponentDidMount} />, 
     document.getElementById("app")
 );
```

#### Post-render component changes

To call SmartClient widget APIs after the component has been rendered, you can just assign the component an ID (which will be passed to the underlying widget), and then use it to refer to the widget in methods.

Here's a modified version of the ["Live Grid" Showcase sample](https://smartclient.com/smartclient-latest/showcase/?id=fetchOperationFS&react) that illustrates the concept:

```
 SC.render(
     <>
         <ListGrid ID="scGrid" dataSource="supplyItem" width="100%" height="200" autoFetchData="true"/>
         <Button top="225" title="Start Editing" click="scGrid.startEditing()"/>
     </>,
     document.getElementById("app")
 );
```
where the button click has been made to call a function that starts a row edit operation on the grid.

If you need to call React component APIs after the component has been rendered, you can use "React refs." Here's the same sample using React refs:

```
 let gridRef = React.createRef();
 let editRow = function () {
     let reactGrid = gridRef.current;
     reactGrid.getSCComponent().startEditing();
 }
 SC.render(
     <>
         <ListGrid dataSource="supplyItem" width="100%" height="200" autoFetchData="true" ref={gridRef}/>
         <Button top="225" title="Start Editing" click={editRow}/>
     </>,
     document.getElementById("app")
 );
```

#### Conditional JSX

We support JSX that contains conditional child elements, such as:

```
 <DynamicForm ID="form1" width="621">
        <fields>
               <TextItem name="text" title="Text" hint="A plain text field" defaultValue=""
                   wrapHintText="false" />
                {showPicker && <ColorItem title="Color Picker" name="colorPicker" />}
                <TextAreaItem name="textArea" title="TextArea" />
        </fields>
 </DynamicForm>
```
as well as conditional JSX in attributes assigned via inlined JavaScript.

We recommend using React refs to reconfigure components after construction, as discussed above, rather than re-rendering conditional JSX child elements, for the best performance, readabillity, and maintainability.

When using conditional JSX, keep in mind:

*   When JSX is re-rendered, React will call **componentDidUpdate()**, which will cause us to apply any detected property changes via [setters](../classes/Class.md#method-classsetproperty). This is limited to [writable properties](../main.md#kb-topic-flag-abbreviations). The underlying SmartClient widget will not be recreated.
*   To destroy and recreate the SC widget in **componentDidUpdate()**, you can set the attribute `recreateOnReactComponentUpdate` true on the component.
*   Alternatively, if you set the `key` attribute on the component to a unique number, that will force React to re-create and remount the component, so that **componentDidMount()** gets called against, recreating the underlying SC widget.
*   When declaring properties that can contain objects, like [Window.headerControls](../classes/Window.md#attr-windowheadercontrols) (a list of strings naming specific controls or Canvas instances), any falsy value will be considered an excluded child element and skipped.
*   For other properties declared with conditional JSX, your conditional element must actually evaluate to `false` to be excluded from the declaration.

For an example of re-rendering, see the ["Saved Search > Built-in" Showcase sample](https://smartclient.com/smartclient-latest/showcase/?id=gridSavedSearchBuiltin&react)

#### Loading Reify screens

Suppose you've created a screen in Reify that you want to load into your React app. You can do it via [Reify.loadProject](#method-reifyloadproject) as in this sample:

```
 let loadProject = function () {
     isc.Reify.loadProject("Test Project", function (project, projects, rpcResponse) {
         isc.RPCManager.getLoadProjectErrorMessage(rpcResponse);
         if (mainLayout.getMembersLength() > 2) mainLayout.removeMember(2);
 
         let screenTitle = project.screens[0].ID,
             screen = project.createScreen(screenTitle);
         mainLayout.addMember(screen);
 
         isc.notify("Reify '" + screenTitle + "' added");
     }, {
         userName: "testuser",
         password: "password",
         serverURL: "https://create.reify.com"
     });
 };
 
 SC.render(
     <VLayout ID="mainLayout" width="100%" height="100%" membersMargin="10"
              defaultLayoutAlign="right">
         <members>
             <Label contents="Loading a screen from Reify into a React Project" height="1"
                    width="100%" align="center" styleName="pageTitle"/>
             <Button name="loadProject" title="Load Project" click={loadProject} />
         </members>  
     </VLayout>,
     document.getElementById("app")
 );
```
which assumes your Reify project is named "Test Project", and that it's in a Reify account with username "testuser" and password "password". When the button is clicked, the first screen from "Test Project" will be added (or replaced) as the last member of the VLayout. For the full sample, please see ["Project Loading" Showcase sample](https://smartclient.com/smartclient-latest/showcase/?id=projectLoadingReify&react).

You can also integrate the Component XML from your Reify screen directly into your React app. Suppose you built a screen in Reify consisting of a button and databound grid, so that clicking the button started editing the grid. If you then clicked on "Show code for screen" in the "More screen actions" menu, you might see the following Component XML:

```
 <DataSources loadID="ApplePie,Customer,Employee,Order,OrderLine,Payment,Product,ProductLine,Sale,Salesperson,Office"/>
 
 <IButton autoID="pressMeButton">
     <title>Press Me</title>
     <click>
         <Action target="officeGrid" name="startEditing"/>
     </click>
 </IButton>
 
 <ListGrid dataSource="Office" autoID="officeGrid" autoFetchData="true">
     <fields>
         <LGField name="officeCode"/>
         <LGField name="city"/>
         <LGField name="phone"/>
         <LGField name="addressLine1"/>
         <LGField name="addressLine2"/>
         <LGField name="state"/>
         <LGField name="country"/>
         <LGField name="postalCode"/>
         <LGField name="territory"/>
     </fields>
 </ListGrid>
 
 <DataView overflow="hidden" autoID="newScreen9" width="100%" height="100%" autoDraw="true">
     <members>
         <Canvas withID="pressMeButton"/>
         <Canvas withID="officeGrid"/>
     </members>
 </DataView>
```
To add this screen to your React app, you'd first need to make sure to load the `Office` DataSource used by the grid, by calling [DataSource.load](../classes/DataSource.md#classmethod-datasourceload) from your app or invoking DataSourceLoader from your app's root HTML.

Then you can just render the Component XML as JSX, remembering to inline the `withID` references since they aren't supported by JSX, and replace the `DataView` with a `VLayout`:

```
 SC.render(
     <VLayout overflow="hidden" width="100%" height="100%" autoDraw="true">
         <members>
             <IButton>
                 <title>Press Me</title>
                 <click>
                     <Action target="officeGrid" name="startEditing"/>
                 </click>
             </IButton>
             <ListGrid dataSource="Office" autoID="officeGrid" autoFetchData="true">
                 <fields>
                     <LGField name="officeCode"/>
                     <LGField name="city"/>
                     <LGField name="phone"/>
                     <LGField name="addressLine1"/>
                     <LGField name="addressLine2"/>
                     <LGField name="state"/>
                     <LGField name="country"/>
                     <LGField name="postalCode"/>
                     <LGField name="territory"/>
                 </fields>
             </ListGrid>
         </members>
     </VLayout>,
     document.getElementById("app")
 );
```
Note that we've dropped the autoID attributes, except for `officeGrid` since we need to refer to it in the button's click method.

#### Mixing React HTML and SmartClient components

SmartClient components can be rendered into any DOM element in your app, not just the root, allowing you to mix React HTML and SmartClient components. For example, consider this modified version of the default App.js file created for a new React app:

```
 import React from 'react';
 import logo from './logo.svg';
 import './App.css';

 import 'smartclient-eval/release';
 import 'smartclient-eval/skins/Tahoe';
 import { Label } from 'smartclient-eval/react';

 function App() {
     return (
         <div className="App">
             <header className="App-header">
             <div id="logo">
                 <img src={logo} className="App-logo" alt="logo" />
             </div>
             <Label backgroundColor="yellow" width="200" height="1" align="center"
                    contents="SmartClient inside" styleName="pageTitle"/>
             <p>
             Edit <code>src/App.tsx</code> and save to reload.
             </p>
             <a className="App-link" href="https://reactjs.org"
                target="_blank" rel="noopener noreferrer">
             Learn React
             </a>
             </header>
         </div>
     );
 }
 export default App;
```
A SmartClient Label (shown in blue above) titled "SmartClient inside" has been added under the React logo. This will appear in the DOM underneath the React logo if the app is run, showing that you can easily mix React HTML and SmartClient components.

DOM elements created by React HTML can also be replaced dynamically. In the sample above, the React logo itself has also been wrapped in a div (shown in green) with the id "logo" so that in another file of the app (or in the click handler of the yellow Label) you can write:

```
 SC.render(
     <Label width="150" height="150" margin="20" backgroundColor="green" border="5px solid #ADD8E6"/>,
     document.getElementById("logo")
 );
```
to replace the logo with a square green SmartClient Label.

#### Custom Components

This section discusses how to extend SmartClient React components to create new custom components. For composition, where you just want to include SmartClient React components in your own component, nothing special like this is required.

To define a custom SmartClient framework subclass and automatically create the corresponding SmartClient React wrapper class, you can just call the `defineClass()` method on the React `SC` utility class:

```
 import React from 'react';
 import ReactDOM from 'react-dom';

 import 'smartclient-eval/release';
 import 'smartclient-eval/skins/Tahoe';
 import { SC, Canvas } from 'smartclient-eval/react';

 let isc = window.isc;

 const MyCanvas = SC.defineClass("MyCanvas", Canvas);
 isc.MyCanvas.addProperties({
     backgroundColor: "purple",
     border: "2px solid red",
     click: "isc.alert('You clicked me!');
 });
```
where the call to `defineClass()` defines the class for you in both React and SmartClient, returning a reference to the React class, so you then must configure your class by calling [addProperties()](../classes/Class.md#method-classaddproperties) on the underlying SmartClient class. This is appropriate if you just want to add specific default properties for your class, or override documented framework methods. See [isc.defineClass()](../classes/ClassFactory.md#classmethod-classfactorydefineclass) for further details.

After this JS, you can declare a `MyCanvas` in your JSX just as if it were a built-in framework React class that you imported:

```
 <MyCanvas width="100" height="200" opacity="20"/>
```

If on the other hand, you want to integrate a completely custom React class around your SmartClient subclass, you'll have to do a bit more work. Instead of calling `SC.defineClass()`, you'll need to explictly define your class with ES6 syntax like:

```
 // ... standard imports (see first sample)
 import { Canvas } from 'smartclient-eval/react';

 let isc = window.isc;
 isc.defineClass("MyCanvas", isc.Canvas).addProperties({
     /// ... customize defaults of underlying SmartClient class
 });

 class MyCanvas extends Canvas {
     static ISC_CLASS_NAME = "MyCanvas";
     static IS_CLASS = true;

     // ... your custom component code
 }
```
and then register it by calling
```
 ReactComponent.registerClass("MyCanvas", MyCanvas);
```

Note that the `isc.defineClass()` call above is only required if you need to also extend the underlying SmartClient class with custom defaults, and have overridden `ISC_CLASS_NAME` in your new React component class. By convention, the underlying SmartClient class is named the same as the React component class that wraps it.

If you create the custom component with `SC.defineClass()` in one place, you can import it elsewhere using `SC.importClass()`. On the other hand, if you decide to declare your new React wrapper class explicitly like "class MyCanvas extends ..." then if you need to use it in multiple files you should move the class definition into its own module, and you can then import it wherever needed using standard ES6 module import syntax.

Your custom React component will typically extend a built-in SmartClient React class, like `Canvas`, but all of the SmartClient React support classes ultimately extend either `IBaseComponent` or `ILogicalComponent`:

*   IBaseComponent. The base class for components that should be rendered in the DOM: ListGrid, Button, etc…
*   ILogicalComponent. The base class for components that should _not_ be rendered in the DOM: LGField, DSField.

Note that `ISC_CLASS_NAME` declares the name of the underlying SmartClient framework class used by your new React component. So if you've not defined such a custom subclass (e.g. via SmartClient framework method [isc.defineClass()](../classes/ClassFactory.md#classmethod-classfactorydefineclass) then you should exclude that line.

Be careful overriding built-in React component methods like `render()`. Often it doesn't make sense to override `render()` when extending a SmartClient React component. For example if you extended the SmartClient React class `Canvas` and then overrode `render()` in that new component class to return <Canvas/> you'd actually be rendering a separate new `Canvas` on top of your new component. If you want to control placement of SmartClient React components, you may be better off building a container via composition.

#### Namespacing

JavaScript ES6 provide built-in namespacing control to your React files via declared imports, so it's unlikely you will have collisions when importing the built-in SmartClient React classes. However, if you do, you can always alias them during import.

So instead of

```
 import { Canvas } from 'smartclient-eval/react';
```
you can write something like
```
 import { Canvas as MyCanvas } from 'smartclient-eval/react';
```
to import one or more classes under other names, or
```
 import * as ReactSC from 'smartclient-eval/react';
```
to import all the SmartClient React classes as a single object. For further details, read about JavaScript import syntax [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import).

#### Further Examples

We've only covered a relatively small range of features above, but all SmartClient features are available, and you can use the full SmartClient Showcase (with over 880 samples) with React. For many Showcase samples, the React JSX version can be shown by [toggling the Showcase to React mode](https://smartclient.com/smartclient-latest/showcase/?react), and for the others, they can be ported to a combination of React JSX and JavaScript by following the [porting guidelines](showcasePorting.md#kb-topic-porting-showcase-samples-to-react).

#### Debugging

Your React app will contain your React components and the React framework, as well as the SmartClient framework and any SmartClient widgets or classes you have defined yourself. All of this will be loaded by your browser as one or more fragments created by webpack. The recommended approach depends on how you want to treat the app:

*   **React App**. Any existing tool designed for React apps can help you. For example, [here](https://raygun.com/blog/react-debugging-guide/) is an introduction to debugging a React app with the browser inspector, with an example. Or, for an overview of how to run Visual Studio Code inside a browser, so you can target a React + SmartClient app, see [this guide](https://code.visualstudio.com/docs/editor/vscode-web).
*   **SmartClient app**. Alternatively, if you know the issue directly relates to SmartClient widgets or APIs, you can look over the SmartClient [debugging](debugging.md#kb-topic-debugging) help topic and use the Developer Console and the techniques there.

#### Server Installation

SmartClient's React support allows you to integrate your React apps client side, but your apps can also use SmartClient's [Java server technology](iscServer.md#kb-topic-smartclient-server-summary), or with any other technology accessible via [REST](../classes/RestDataSource.md#class-restdatasource), [WSDL](wsdlBinding.md#kb-topic-wsdl-binding) or [HTTP](platformDependencies.md#kb-topic-platform-dependencies) in general.

### See Also

- [reactIntegration](reactIntegration.md#kb-topic-integrating-pre-existing-smartclient-apps-with-react)
- [showcasePorting](showcasePorting.md#kb-topic-porting-showcase-samples-to-react)

---
