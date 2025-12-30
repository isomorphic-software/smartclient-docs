# Visual Builder

[← Back to API Index](../reference.md)

---

## KB Topic: Visual Builder

### Description
The SmartClient Visual Builder tool is intended for:

*   business analysts and others doing functional application design, who want to create functional prototypes in a codeless, "what you see is what you get" environment
*   developers new to SmartClient who want to get a basic familiarity with component layout, component properties and SmartClient code structure
*   developers building simple applications that can be completed entirely within Visual Builder

**Visual Builder for Functional Design**

Visual Builder has several advantages over other tools typically used for functional design:

*   Visual Builder allows simple drag and drop manipulation of components, form-based editing of component properties, and simple connection of events to actions - all without requiring any code to be written. It is actually simpler to use than DreamWeaver or other code-oriented prototyping tools
*   because Visual Builder generates clean code, designs will not have to be converted to another technology before development can proceed. This reduces both effort and the potential for miscommunication
*   developers can add custom skinning, components with custom behaviors, and custom DataSources with sample datasets to Visual Builder so that the design environment is an even closer match to the final application. This helps eliminate many types of unimplementable designs
*   because Visual Builder is built in SmartClient itself, Visual Builder is simply a web page, and does not require installation. Visual Builder can be deployed to an internal network to allow teams with a mixture of technical and semi-technical users to collaboratively build and share prototypes of SmartClient-based applications.

#### Launching & Using Visual Builder

The SmartClient SDK already has Visual Builder installed - access it from the SDK Explorer under Tools -> Visual Builder (see QuickStart Guide for how to access the SDK Explorer).

Basic usage instructions are embedded in Visual Builder itself, in the "About Visual Builder" pane. Click on it to open it.

**Loading and Saving**

The "Project" pane within Visual Builder allows screens to be saved and reloaded for further editing. Saved screens **can** be edited outside of Visual Builder and successfully reloaded, however, as with any design tool that provides a drag and drop, dialog-driven approach to screen creation, Visual Builder cannot work with entirely free-form code. In particular, when a screen is loaded and then re-saved:

*   any indenting or spacing changes are not preserved
*   order of property or method definitions will revert to Visual Builder's default
*   while method definitions on components are preserved, any code **outside of** component definitions will be dropped (in some cases adding such code will cause loading to fail)
*   each Canvas-based component will be output separately, in the order these components appear in the project tree, deepest first

Generally speaking, screen definitions that you edit within Visual Builder should consist of purely declarative code. Rather than appearing in screen definitions, custom components and JavaScript libraries should be added to Visual Builder itself via the customization facilities described below.

#### Installing Visual Builder

Visual Builder comes already installed and working in the SDK, and can be used from there out of the box. This is the simplest thing to do during initial prototyping.

Further on in the development cycle, it may be advantageous to have Visual Builder available outside the SDK, for example in your test environment. Installing Visual Builder into such an environment is very easy:

*   Perform a normal installation procedure, as discussed [here](iscInstall.md#kb-topic-deploying-smartclient)
*   Copy the following .jar files from the SDK `lib` folder to the target `WEB-INF/lib` folder:
    *   `isomorphic_tools.jar`
    *   `isomorphic_sql.jar`
    *   `isomorphic_hibernate.jar`
*   Copy the SDK `tools` folder to the target application root

Note that it is safe to include Visual Builder even in a production environment, so long as you ensure that the `tools` folder is protected with any normal HTTP authentication/authorization mechanism - for example, an authentication filter.

#### Customizing Visual Builder

The rest of this topic focuses on how Visual Builder can be customized and deployed by developers to make it more effective as a functional design tool for a particular organization.

**Adding Custom DataSources to Visual Builder**

DataSources placed in the project dataSources directory (\[webroot\]/shared/ds by default) will be detected by Visual Builder whenever it is started, and appear in the DataSource listing in the lower right-hand corner automatically.

If you have created a custom subclass of DataSource (eg, as a base class for several DataSources that contact the same web service), you can use it with Visual Builder by:

*   creating an XML version of the DataSource using the XML tag `<DataSource>` and the `constructor` property set to the name of your custom DataSource subclass (as described [componentXML](componentXML.md#kb-topic-component-xml) under the heading _Custom Components_)
*   modifying \[webroot\]/tools/visualBuilder/globalDependencies.xml to load the JavaScript code for your custom DataSource class. See examples in that file.

**Adding Custom Components to Visual Builder**

The Component Library on the right hand side of Visual Builder loads component definitions from two XML files in the \[webroot\]/tools/visualBuilder directory: customComponents.xml and defaultComponents.xml. customComponents.xml is empty and is intended for developers to add their own components. defaultComponents.xml can also be customized, but the base version will change between SmartClient releases.

As can be seen by looking at defaultComponents.xml, components are specified using a tree structure similar to that shown in the *tree XML loading example*. The properties that can be set on nodes are:

*   `type`: name of the SmartClient Class on which [create()](../classes/Class.md#classmethod-classcreate) will be called in order to construct the component. `type` can be omitted to create a folder that cannot be dropped
*   `title`: title for the node
*   `defaults`: an Object specifying defaults to be passed to [create()](../classes/Class.md#classmethod-classcreate). For example, you could add an "EditableGrid" node by using `type: "ListGrid"` and specifying:
    ```
     <defaults canEdit="true"/>
    ```
    NOTE: if you set any defaults that are not Canvas properties, you need to provide explicit type as documented under _Custom Properties_ for [componentXML](componentXML.md#kb-topic-component-xml).
*   `children`: components that should appear as children in the tree under this node
*   `icon`: icon to show in the Visual Builder component tree (if desired)
*   `iconWidth/Height/Size`: dimensions of the icon in pixels ("iconSize" sets both)
*   `showDropIcon`: for components that allow children, whether to show a special drop icon on valid drop (like [TreeGrid.showDropIcons](../classes/TreeGrid.md#attr-treegridshowdropicons)).

In order to use custom classes in Visual Builder, you must modify `[webroot]/tools/visualBuilder/globalDependencies.xml` to include:

*   the JavaScript class definition for the custom class (in other words, the [defineClass()](../classes/isc.md#staticmethod-iscdefineclass) call)
*   a [component schema](componentSchema.md#kb-topic-component-schema) for the custom component

See globalDependencies.xml for examples.

#### Component Schema and Visual Builder

When you provide [custom schema](componentSchema.md#kb-topic-component-schema) for a component, Visual Builder uses that schema to drive component editing (Component Properties pane) and to drive drag and drop screen building functionality.

**Component Editing**

Newly declared fields will appear in the Component Editor in the "Other" category at the bottom by default. You can create your own category by simply setting field.group to the name of a new group and using this on multiple custom fields.

The ComponentEditor will pick a FormItem for a custom field by the [same rules](../reference_2.md#type-formitemtype) used for ordinary databinding, including the ability to set field.editorType to use a custom FormItem.

When properties are changed by the user, Visual Builder will look for an appropriate "setter function" for the custom field, for example, for a field named "myProp", Visual Builder will look for "setMyProp". The target component will also be [redrawn](../classes/Canvas.md#method-canvasredraw).

**Event -> Action Bindings**

The Component Properties pane contains an Events tab that allows you wire components events to actions on any other component currently in the project.

Events are simply [StringMethods](../reference.md#kb-topic-string-methods-overview) defined on the component. In order to be considered events, method definitions must have been added to the class via [Class.registerStringMethods](../classes/Class.md#classmethod-classregisterstringmethods) and either be publicly documented SmartClient methods or, for custom classes, have a methods definition in the [component schema](componentSchema.md#kb-topic-component-schema). Examples of events are: [ListGrid.recordClick](../classes/ListGrid_2.md#method-listgridrecordclick) and [DynamicForm.itemChange](../classes/DynamicForm.md#method-dynamicformitemchange).

Actions are methods on any component that have a method definition in the [component schema](componentSchema.md#kb-topic-component-schema) and specify action="true".

All available events (stringMethods) on a component are shown in the Events tab of the Component Editor. Clicking the plus (+) sign next to the event name brings up a menu that shows a list of all components currently in the project and their available actions. Selecting an action from this submenu binds the action to the selected event. When an event is bound to an action in this manner, automatic type matching is performed to pass arguments from the event to the action as follows:

*   Only non-optional parameters of the action are bound.
*   For each non-optional parameter of the action method, every parameter of the event method is inspected in order to either directly match the type (for non-object types) or to match an isAssignableFrom type check via a SmartClient schema inheritance check.
*   The 'type' of a parameter is determined from the type documented in the SmartClient reference for built-in components, or from the `type` attribute on the method param in the [component schema](componentSchema.md#kb-topic-component-schema) definition of a custom component.
*   When a matching parameter is found, it is assigned to the current slot of the action and not considered for further parameter matching.
*   The above pattern is repeated until all non-optional parameters are exhausted, all event parameters are exhausted, or until no further type matches can be inferred.

The "actionBinding" log category can be enabled in the Developer Console to troubleshoot issues with automatic binding for custom methods.

**Component Drag and Drop**

Visual Builder uses component schema to determine whether a given drop is allowed and what methods should be called to accomplish the drop. For example, any Canvas-based component can be dropped on a VLayout because VLayout has a "members" field of type "Canvas", and an [addMember()](../classes/Layout.md#method-layoutaddmember) function.

Because of these rules, any subclass of Canvas will be automatically eligible to be dropped into any container that accepts a Canvas (eg, a Layout or Tab). Any subclass of a FormItem will be, likewise, automatically eligible to be dropped into a DynamicForm.

You can declare custom containment relations, such as a custom class "Wizard" that accepts instances of the custom class "Pane" by simply declaring a [component schema](componentSchema.md#kb-topic-component-schema) that says that Wizard has a property called "panes" of type "Pane". Then, provide methods that allow components to be added and removed:

*   for a [multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple) field, provide "add" and "remove" functions based on the name of the field. For example, for a field "panes" of type "Pane", provide "addPane()" that takes a Pane instance, and "removePane()" that takes a pane instance or pane ID
*   for a singular field (such as [Canvas.contextMenu](../classes/Canvas.md#attr-canvascontextmenu) or [Tab.pane](../classes/Tab.md#attr-tabpane)), provide a setter method named after the field (eg setContextMenu()) that takes either an instance of the component or null for removal

The "editing" log category can be enabled in the Developer Console to troubleshoot issues with schema-driven drag and drop and automatic lookup of getter/setter and adder/remover methods.

**NOTE:** after modifying component schema, it may be necessary to restart the servlet engine and reload Visual Builder

**Presenting simplified components**

SmartClient components expose many methods and properties. For some environments, it is more appropriate to provide a simplified list of properties, events, and actions on either built-in SmartClient components or your custom components. This can be done by providing a custom [component schema](componentSchema.md#kb-topic-component-schema) for an existing component that exposes your minimal set. You also need to provide a trivial subclass of the class you're exposing so that it can be instantiated.

For example, let's say you want to make a simplified button called EButton that exposes only the 'title' property and the 'click' event of a standard Button. The following steps will accomplish this:

1\. Edit /tools/visualBuilder/customComponents.xml and add a block similar to the following to make your custom component appear in the Component Library:

```
 <PaletteNode>
     <title>EButton</title>
     <type>EButton</type>
     <icon>button.gif</icon>
 </PaletteNode>
 
```
2\. Next, create a custom schema: /isomorphic/system/schema/EButton.ds.xml as follows:
```
 <DataSource ID="EButton" inheritsFrom="Button" Constructor="EButton"
             showLocalFieldsOnly="true" showSuperClassActions="false"
             showSuperClassEvents="false">
 	   <fields>
         <field name="title"  type="HTML"/>
     </fields>
     <methods>
         <method name="click">
             <description>Fires when this button is clicked.</description>
         </method>
     </methods>
 </DataSource>
 
```
See documentation above and also [component schema](componentSchema.md#kb-topic-component-schema) for what the properties above do. 3. Finally, you'll need to define an EButton class as a simple subclass of Button, as follows:
```
 isc.defineClass("EButton", "Button");
 
```
To make sure that the Visual Builder will load the above definition, you'll need to place it into a JavaScript file being loaded by the Visual Builder. If you do not already have such a file, you can create one and add it to the list of Visual Builder dependencies by adding an entry in /tools/visualBuilder/globalDependencies.xml. See examples in that file for specifics.

### Related

- [VisualBuilder](../classes/VisualBuilder.md#class-visualbuilder)

### See Also

- [toolsDeployment](toolsDeployment.md#kb-topic-tools-deployment)

---
