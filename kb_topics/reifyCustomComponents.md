# Adding Custom Components to Reify

[← Back to API Index](../reference.md)

---

## KB Topic: Adding Custom Components to Reify

### Description
Reify is a web-based visual application builder that enables non-developers to build SmartClient screens, and even build complete applications.

You can customize Reify by adding your own custom components, and even adding custom editors for properties of those components.

The following instructions are for customizing a [Reify OnSite](reifyOnSite.md#kb-topic-reify-onsite) instance. It's also possible to customize your account at Reify.com - to do that, please contact Isomorphic [here](https://www.reify.com/contactus.jsp).

**Component Library**

Reify has the ability to include new component classes defined in JavaScript, in addition to the set of components available by default.

The Component Library on the right hand side of Reify loads component definitions from two XML files in the \[webroot\]/tools/visualBuilder directory: customComponents.xml and defaultComponents.xml. customComponents.xml is empty and is intended for developers to add their own components. defaultComponents.xml can also be customized, but the base version will change between SmartClient releases.

As can be seen by looking at defaultComponents.xml, components are specified using a tree structure similar to that shown in the *tree XML loading example*. The properties that can be set on nodes are:

*   `type`: name of the SmartClient Class on which [create()](../classes/Class.md#classmethod-classcreate) will be called in order to construct the component. `type` can be omitted to create a folder that cannot be dropped
*   `title`: title for the node
*   `defaults`: an Object specifying defaults to be passed to [create()](../classes/Class.md#classmethod-classcreate). For example, you could add an "EditableGrid" node by using `type: "ListGrid"` and specifying:
    ```
     <defaults canEdit="true"/>
    ```
    NOTE: if you set any defaults that are not Canvas properties, you need to provide explicit type as documented under _Custom Properties_ for [componentXML](componentXML.md#kb-topic-component-xml).
*   `children`: components that should appear as children in the tree under this node
*   `icon`: icon to show in the Reify component tree (if desired)
*   `iconWidth/Height/Size`: dimensions of the icon in pixels ("iconSize" sets both)
*   `showDropIcon`: for components that allow children, whether to show a special drop icon on valid drop (like [TreeGrid.showDropIcons](../classes/TreeGrid.md#attr-treegridshowdropicons))
*   and additional properties described on [PaletteNode](../reference.md#object-palettenode).

In order to use custom classes in Reify, you must modify `[webroot]/tools/visualBuilder/globalDependencies.xml` to include:

*   the JavaScript class definition for the custom class (in other words, the [defineClass()](../classes/isc.md#staticmethod-iscdefineclass) call)
*   a [component schema](componentSchema.md#kb-topic-component-schema) for the custom component

See globalDependencies.xml for examples.

#### Component Schema and Reify

When you provide [custom schema](componentSchema.md#kb-topic-component-schema) for a component, Reify uses that schema to drive component editing (Component Properties pane) and to drive drag and drop screen building functionality.

**Component Editing**

Newly declared fields will appear in the Component Editor in the "Other" category at the bottom by default. You can create your own category by simply setting field.group to the name of a new group and using this on multiple custom fields.

The ComponentEditor will pick a FormItem for a custom field by the [same rules](../reference.md#type-formitemtype) used for ordinary databinding, including the ability to set field.editorType to use a custom FormItem.

When properties are changed by the user, Reify will look for an appropriate "setter function" for the custom field, for example, for a field named "myProp", Reify will look for "setMyProp". The target component will also be [redrawn](../classes/Canvas.md#method-canvasredraw).

**Designing Components for Editing & Using Placeholders**

When Reify creates your custom component, no properties are provided at construction, and all necessary properties will be provided after construction via calling setter methods (for example, `set_PropertyName_`) as users assign them via the Property Sheet.

Often a custom component has been implemented to expect that certain properties are passed at construction, and the constructor may crash if they are absent. Similarly, setters may not exist for properties assumed to be provided at construction, or may crash. Any such errors are caught by Reify and reported under the "componentExceptions" log category, however, Reify has several features to make it possible to work with misbehaving components without requiring refactoring.

If a component requires certain properties before it can be validly created, you can set [PaletteNode.requiredProperties](../classes/PaletteNode.md#attr-palettenoderequiredproperties) as a comma-separated list of property names on the `paletteNode` for the component, and Reify will use a placeholder until the designer has provided each of the required properties. The placeholder will just show the className of the real component and the list of remaining required properties. In order to take up the right amount of space, the placeholder will use the same sizing-related settings that the real component would use (such as `overflow` and `defaultWidth`).

If a component lacks appropriate setters for some properties but would work properly if re-created from scratch, in the Component Schema you can set [DataSourceField.recreateOnChange](../classes/DataSourceField.md#attr-datasourcefieldrecreateonchange) on any fields that should cause the component to be re-created. You can also set [PaletteNode.recreateOnChange](../classes/PaletteNode.md#attr-palettenoderecreateonchange) on a `paletteNode` to cause **any** property change to cause the component to be re-created.

You may also have components that you don't want to try to use within Reify at all. In this case, just set [PaletteNode.alwaysUsePlaceholder](../classes/PaletteNode.md#attr-palettenodealwaysuseplaceholder) to true, and Reify will never try to create the component, and always show a placeholder. You can also set [PaletteNode.placeholderImage](../classes/PaletteNode.md#attr-palettenodeplaceholderimage) to the URL of an image file to use in lieu of the usual placeholder text.

Note that when you use the Run within Reify, Placeholders will appear (otherwise your screen would presumably crash!) - this is because Reify is using the [LoadProjectSettings.allowPlaceholders](../classes/LoadProjectSettings.md#attr-loadprojectsettingsallowplaceholders) option. If you export a Reify project or [load it dynamically](#method-reifyloadproject), `allowPlaceholders` will be false, and your screen will use the real target components.

**Event -> Action Bindings**

The Component Properties pane contains an Events tab that allows you wire components events to actions on any other component currently in the project.

Events are simply [StringMethods](stringMethods.md#kb-topic-string-methods-overview) defined on the component. In order to be considered events, method definitions must have been added to the class via [Class.registerStringMethods](../classes/Class.md#classmethod-classregisterstringmethods) and either be publicly documented SmartClient methods or, for custom classes, have a methods definition in the [component schema](componentSchema.md#kb-topic-component-schema). Examples of events are: [ListGrid.recordClick](../classes/ListGrid_2.md#method-listgridrecordclick) and [DynamicForm.itemChange](../classes/DynamicForm.md#method-dynamicformitemchange).

Actions are methods on any component that have a method definition in the [component schema](componentSchema.md#kb-topic-component-schema) and specify action="true".

All available events (stringMethods) on a component are shown in the Events tab of the Component Editor. Clicking the plus (+) sign next to the event name brings up a menu that shows a list of all components currently in the project and their available actions. Selecting an action from this submenu binds the action to the selected event. When an event is bound to an action in this manner, automatic type matching is performed to pass arguments from the event to the action as follows:

*   Only non-optional parameters of the action are bound.
*   For each non-optional parameter of the action method, every parameter of the event method is inspected in order to either directly match the type (for non-object types) or to match an isAssignableFrom type check via a SmartClient schema inheritance check.
*   The 'type' of a parameter is determined from the type documented in the SmartClient reference for built-in components, or from the `type` attribute on the method param in the [component schema](componentSchema.md#kb-topic-component-schema) definition of a custom component.
*   When a matching parameter is found, it is assigned to the current slot of the action and not considered for further parameter matching.
*   The above pattern is repeated until all non-optional parameters are exhausted, all event parameters are exhausted, or until no further type matches can be inferred.

The "actionBinding" log category can be enabled in the Developer Console to troubleshoot issues with automatic binding for custom methods.

**Component Drag and Drop**

Reify uses component schema to determine whether a given drop is allowed and what methods should be called to accomplish the drop. For example, any Canvas-based component can be dropped on a VLayout because VLayout has a "members" field of type "Canvas", and an [addMember()](../classes/Layout.md#method-layoutaddmember) function.

Because of these rules, any subclass of Canvas will be automatically eligible to be dropped into any container that accepts a Canvas (eg, a Layout or Tab). Any subclass of a FormItem will be, likewise, automatically eligible to be dropped into a DynamicForm.

You can declare custom containment relations, such as a custom class "Wizard" that accepts instances of the custom class "Pane" by simply declaring a [component schema](componentSchema.md#kb-topic-component-schema) that says that Wizard has a property called "panes" of type "Pane". Then, provide methods that allow components to be added and removed:

*   for a [multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple) field, provide "add" and "remove" functions based on the name of the field. For example, for a field "panes" of type "Pane", provide "addPane()" that takes a Pane instance, and "removePane()" that takes a pane instance or pane ID
*   for a singular field (such as [Canvas.contextMenu](../classes/Canvas.md#attr-canvascontextmenu) or [Tab.pane](../classes/Tab.md#attr-tabpane)), provide a setter method named after the field (eg setContextMenu()) that takes either an instance of the component or null for removal

The "editing" log category can be enabled in the Developer Console to troubleshoot issues with schema-driven drag and drop and automatic lookup of getter/setter and adder/remover methods.

**NOTE:** after modifying component schema, it may be necessary to restart the servlet engine and reload Reify

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
See documentation above and also [component schema](componentSchema.md#kb-topic-component-schema) for what the properties above do.

3\. Finally, you'll need to define an EButton class as a simple subclass of Button, as follows:

```
 isc.defineClass("EButton", "Button");
 
```
To make sure that Reify will load the above definition, you'll need to place it into a JavaScript file being loaded by Reify. If you do not already have such a file, you can create one and add it to the list of Reify dependencies by adding an entry in /tools/visualBuilder/globalDependencies.xml. See examples in that file for specifics.

### See Also

- [toolsDeployment](toolsDeployment.md#kb-topic-tools-deployment)
- [reifyCustomComponents](#kb-topic-adding-custom-components-to-reify)
- [reifyCustomDataSources](reifyCustomDataSources.md#kb-topic-adding-custom-datasources-to-reify)

---
