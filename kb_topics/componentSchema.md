# Component Schema

[← Back to API Index](../reference.md)

---

## KB Topic: Component Schema

### Description
A component schema is a special type of DataSource that describes a custom component.

Declaring a component schema for your custom component allows you to:

*   use simpler XML when creating your custom component: avoid having to specify the `constructor` and `xsi:type` attributes as described under [componentXML](componentXML.md#kb-topic-component-xml)
*   use your custom component within [Reify](reify.md#kb-topic-reify-overview)

**Example of a Component Schema**

In its most basic form, a component schema for a custom subclass of ListGrid called "MyListGrid" looks like this:

```
 <DataSource serverType="component" ID="MyListGrid" 
             inheritsFrom="ListGrid" instanceConstructor="MyListGrid"/>
 
```
With this definition saved as "MyListGrid.ds.xml" in the project dataSources directory (\[webroot\]/shared/ds/ by default), you can now create an instance of MyListGrid with just:
```
 <MyListGrid width="500"/>
 
```
Note: you may need to restart your servlet engine/J2EE container before this example will work.

The attributes set directly on the DataSource tag have special meaning for a component schema definition:

*   [serverType](../classes/DataSource.md#attr-datasourceservertype)="component" indicates this DataSource describes a component, as opposed to a SQL table or other data provider
*   [ID](../classes/DataSource.md#attr-datasourceid) means the tagName that will be used to create your custom component. This must match the first component of the filename. (ID="MyListGrid" means the filename must be MyListGrid.ds.xml, and typically also matches the name of the class).
*   [DataSource.inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom)="ListGrid" inherits the ListGrid property definitions via [DataSource.inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom).
*   instanceConstructor="MyListGrid" indicates the SmartClient class that [create()](../classes/Class.md#classmethod-classcreate) should be called on to construct an instance.
*   showLocalFieldsOnly is a boolean that, when set to true, tells the [Reify](reify.md#kb-topic-reify-overview) to show only the fields declared in this schema in the component editor. Otherwise fields inherited via [DataSource.inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom) (all the way up the chain) are also included.
*   showSuperClassEvents is a boolean that, like showLocalFieldsOnly, optionally restricts the list of events shown in the Events tab of the [Reify](reify.md#kb-topic-reify-overview) to those defined in this schema only.
*   showSuperClassActions is a boolean that optionally restricts the list of actions shown in the menu when you map a component Event to a component Action within [Reify](reify.md#kb-topic-reify-overview) to those defined in this schema only.

**Declaring custom properties**

Custom properties are declared via [fields](../classes/DataSource.md#attr-datasourcefields) as for an ordinary [DataSource](../classes/DataSource.md#class-datasource). As with ordinary DataSources, it is legal to redeclare inherited fields in order to modify properties such as [field.editorType](../classes/DataSourceField.md#attr-datasourcefieldeditortype).

The following DataSourceField properties have special significance when a component schema is used to process [component XML](componentXML.md#kb-topic-component-xml):

*   [field.type](../classes/DataSourceField.md#attr-datasourcefieldtype) declares the type of the field, and hence the type of the JavaScript value your custom class will be initialized with. In order to declare subcomponents, can be set to the name of another component (built-in or custom).
*   [field.multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple) declares that the field should always be array-valued even when only a single value is provided. Also indicates that the field name should be used as a "wrapper tag" in the XML format for the component.
*   [field.propertiesOnly](../classes/DataSourceField.md#attr-datasourcefieldpropertiesonly). For fields that hold subcomponents, suppresses auto-construction to avoid [double drawing](../classes/Canvas.md#attr-canvasautodraw) and to allow subcomponents to be modified by their parent component before they are created and drawn

When a component is edited within Reify, the DataSource properties that normally influence databound forms will influence the Component Editor (for example, field.title, field.editorType). In addition, the following properties have special significance in component editing and component drag and drop:

*   [field.inapplicable](../classes/DataSourceField.md#attr-datasourcefieldinapplicable) indicates that an inherited field is inapplicable in this component.
*   [field.group](../classes/DataSourceField.md#attr-datasourcefieldgroup) indicates what group the property should be placed in when editing in Reify.
*   [field.xmlAttribute](../classes/DataSourceField.md#attr-datasourcefieldxmlattribute): indicates this field should serialize as an XML attribute. Note that when constructing the component from XML, either an attribute or a subelement will continue to be accepted as means of specifying the field value, so this property is primarily set in order to make code generated by Reify maximally compact or to make it conform to externally set standards.

**Declaring Events and Actions**

Events and Actions are declared via a methods array. In order for a method to be considered an event, it needs to have a method definition in the methods array (or be publicly documented in the SmartClient reference) and have been added to the class as a [StringMethod](stringMethods.md#kb-topic-string-methods-overview) via [Class.registerStringMethods](../classes/Class.md#classmethod-classregisterstringmethods).

In order for a method to be considered an action, it needs to have a method definition in the methods array and have the `action` property set to `true`. For example, the following is a definition of the 'hide' action available on any Canvas, as copied from Canvas.ds.xml:

```
     <methods>
         <method name="hide" title="Hide" action="true"/>
     </methods>
 
```
For custom component actions, an array of expected parameters may be specified using the `params` attribute. Each entry in this array should have a specified type. By doing this, you allow the Reify to pass parameters through to actions when setting up events that call actions (possibly on another component). For example if you had a component with a custom action that expected to be passed a single parameter of type [ListGridRecord](../reference_2.md#object-listgridrecord) you could define it as follows:
```
     <method name="showRecordDetails" title="Show Record Details" action="true">
         <params>
             <param type="ListGridRecord"/>
         <params>
     </method>
 
```
If a user working within the Reify then added ListGrid to the page and used the "+" icon to associate the [recordClick](../classes/ListGrid_2.md#method-listgridrecordclick) event with this custom method, the Reify logic would automatically associate the parameters available in the fired event (in this case `recordClick`) with the expected parameters for the action to fire by type. So the `record` parameter of the event (known to be of type `ListGridRecord`) would be passed through to this custom _showRecordDetails_ action as the first parameter.

### Related

- [DataSourceField.xmlAttribute](../classes/DataSourceField.md#attr-datasourcefieldxmlattribute)
- [DataSourceField.childTagName](../classes/DataSourceField.md#attr-datasourcefieldchildtagname)
- [DataSourceField.propertiesOnly](../classes/DataSourceField.md#attr-datasourcefieldpropertiesonly)
- [DataSourceField.inapplicable](../classes/DataSourceField.md#attr-datasourcefieldinapplicable)
- [DataSourceField.group](../classes/DataSourceField.md#attr-datasourcefieldgroup)
- [DataSourceField.recreateOnChange](../classes/DataSourceField.md#attr-datasourcefieldrecreateonchange)
- [DataSourceField.multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple)

---
