# Class Documentation

[← Back to API Index](../reference.md)

---

## Class: Class

### Description
The Class object is root of the Isomorphic SmartClient inheritance tree -- it includes functionality for creating instances, adding methods and properties, getting prototypes, etc.  
  
To add functionality to ALL classes, add them to Class.  
  
To create a Class, call `ClassFactory.defineClass("MyClass", "MySuperClass")`

`defineClass` will return the created class, and make it available as `isc.MyClass`, and as the global variable `MyClass` if not in [portal mode](../reference.md#object-isc).

You can then:

*   add class-level (static) properties and methods to the class: `MyClass.addClassProperties()` these methods and properties are accessed through the Class variable itself, eg: `MyClass.someStaticMethod()` or `MyClass.someStaticProperty`
*   add default instance properties and methods to the class: `MyClass.addProperties()` these methods and properties are accessed through a class instance, eg: `var myInstance = MyClass.create();` `myInstance.someInstanceMethod()`
*   create new instances of this class: `var myInstance = MyClass.create()`

NOTE: as a convention, all class names begin with a capital letter and all instances begin with a lower case letter.

---
## ClassAttr: Class.isFrameworkClass

### Description
Is this a core SmartClient class (part of the SmartClient framework)? This attribute may be used for debugging, and by the AutoTest subsystem to differentiate between SmartClient classes (part of the smartClient framework) and subclasses created by specific applications

### Groups

- autoTest

**Flags**: RWA

---
## Attr: Class.autoCreator

### Description
Specifies the component on which [Class.createAutoChild](#method-classcreateautochild) should be called to create [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren) defined lazily on this component in the format "autoChild:_autoChildName_". This property may be either specified as a live component, or set to the `_childName_` of another already-created AutoChild.

If left unspecified, the Framework applies rules to determine which component to use as the creator. If this component is itself an autochild, and properties or defaults for the child are defined on its [Class.creator](#attr-classcreator) but not on the component itself, then the creator of this component is also used to create the new AutoChild. Otherwise, this component is used.

### Groups

- autoChildren

### See Also

- [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren)

**Flags**: IRA

---
## Attr: Class.dynamicProperties

### Description
Object mapping dynamic property names to the source - a [DataPath](../reference_2.md#type-datapath), [UserSummary](../reference.md#object-usersummary), [UserFormula](../reference.md#object-userformula), or [AdvancedCriteria](../reference.md#object-advancedcriteria). This is a declarative alternative to calling [Class.addDynamicProperty](#method-classadddynamicproperty) for each property.

See [Class.addDynamicProperty](#method-classadddynamicproperty) for details on using dynamic properties.

In JavaScript dynamicProperties can be declaratively initialized as follows:

```
 dynamicProperties: {
     propName1: "a/b/c",
     propName2: { formula: .. formula definition .. },
     propName3: { textFormula: .. summary definition .. },
     propName4: { operator: "and",
                  criteria: [{
                      fieldName: "a/b/c", operator:"greaterOrEqual", value:"value1"
                  }, {
                      fieldName: "a/b/c", operator:"lessOrEqual", value:"value2"
                  }]
                }
 }
 
```

In ComponentXML dynamicProperties can be intialized as:

```
 <dynamicProperties>
     <property name="propName" dataPath="a/b/c"/>
     <property name="propName2">
         <formula>
             <UserFormula ... >
         </formula>
     </property>
     <property name="propName3">
         <textFormula>
             <UserSummary ... >
         </textFormula>
     </property>
     <property name="propName4">
         <trueWhen>
             <criteria fieldName="a/b/c" operator="iEquals" value="value1"/>
         </trueWhen>
     </property>
     <property name="propName5">
         <trueWhen>
             <AdvancedCriteria operator="and">
                 <criteria>
                     <criterion fieldName="a/b/c" operator="greaterOrEqual" value="value1"/>
                     <criterion fieldName="a/b/c" operator="lessOrEqual"    value="value2"/>
                 </criteria>
             </AdvancedCriteria>
         </trueWhen>
     </property>
 </dynamicProperties>
 
```

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [Class.addDynamicProperty](#method-classadddynamicproperty)

**Flags**: IR

---
## Attr: Class.ruleScope

### Description
[Canvas.ID](Canvas.md#attr-canvasid) of the component that manages "rule context" for which this class participates. A non-Canvas class can only use the ruleScope for supporting [Class.dynamicProperties](#attr-classdynamicproperties). Unlike [Canvas.ruleScope](Canvas.md#attr-canvasrulescope) `ruleScope` on a standalone class must be explicitly specified.

### See Also

- [Canvas.ruleScope](Canvas.md#attr-canvasrulescope)

**Flags**: IR

---
## Attr: Class.addPropertiesOnCreate

### Description
Controls whether arguments passed to [Class.create](#classmethod-classcreate) are assumed to be Objects containing properties that should be added to the newly created instance. This behavior is how `create()` works with almost all SmartClient widgets and other components, allowing the convenient shorthand of setting a batch of properties via an [JavaScript Object Literal](../reference.md#type-objectliteral) passed to create().

The setting defaults to true if unset. To disable this behavior for a custom class, such that `create()` works more like typical constructors found in Java and other languages, use:

```
     isc.[i]ClassName[/i].addProperties({ addPropertiesOnCreate:false })
 
```

Note that it is not valid to disable this behavior for any subclass of [Canvas](Canvas.md#class-canvas) (Canvas relies on this property).

Regardless of the setting for `addPropertiesOnCreate`, all arguments passed to [Class.create](#classmethod-classcreate) are still passed on to [Class.init](#method-classinit).

**Flags**: RA

---
## Attr: Class.unnamedFieldTitle

### Description
Substitute title to use for a title-less, unnamed field.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: Class.creator

### Description
For an [AutoChild](../kb_topics/autoChildren.md#kb-topic-autochildren), a read-only reference to the component on which [Class.createAutoChild](#method-classcreateautochild) or [Class.addAutoChild](#method-classaddautochild) was called to create it. Useful for authoring of event handlers (eg click:"this.creator.doSomething()")

### Groups

- autoChildren

### See Also

- [Class.autoCreator](#attr-classautocreator)

**Flags**: R

---
## Attr: Class.unknownFieldTitle

### Description
Substitute title to use for an unknown field.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassMethod: Class.changeDefaults

### Description
Changes a set of defaults defined as a JavaScript Object. For these kind of properties, simply calling [Class.addProperties](#method-classaddproperties) would replace the original Object with yours, wiping out settings required for the basic functionality of the component. This method instead applies your overrides over the existing properties, without destroying non-overridden properties.

For example let's say you have a component that's defined as follows

```
 isc.defineClass("MyComponent");
 isc.MyComponent.addProperties({
     simpleProperty: "some value",
     propertyBlock : {
       foo: "bar",
       zoo: "moo"
     }
 }
 
```
If you wanted to override simpleProperty, you can just call [Class.addProperties](#method-classaddproperties) like this:
```
 isc.MyComponent.addProperties({
     simpleProperty: "my override"
 });
 
```
If you want to override the value of `propertyBlock.moo` above, but you don't want to clobber the value of `propertyBlock.zoo`. If you use the above pattern like so:
```
 isc.MyComponent.addProperties({
     propertyBlock: {
         foo: "new value",
         zoo: "moo"
     }
 });
 
```
You need to re-specify the value of `propertyBlock.zoo` which you didn't want to override. Failing to re-specify it would destroy the value.

Instead of re-specifying the value, you can use this method to modify the value of `foo` - like this:

```
 isc.MyComponent.changeDefaults("propertyBlock", {
     foo: "new value"
 });
 
```

See also the [AutoChild](../reference.md#type-autochild) system for information about standard sets of defaults that are available for customization.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultsName | [String](#type-string) | false | — | name of the property to change |
| newDefaults | [Object](../reference.md#type-object) | false | — | overrides for defaults |

**Flags**: A

---
## ClassMethod: Class.fireCallback

### Description
Fire some arbitrary action specified as a [Callback](../reference.md#type-callback). Returns the value returned by the action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | Action to fire. |
| argNames | [String](#type-string) | true | — | Comma separated string of variable names. If the callback passed in was a string of script, any arguments passed to the callback will be available as local variables with these names. |
| args | [Array](#type-array) | true | — | Array of arguments to pass to the method. Note that the number of arguments should match the number of argNames. |
| target | [Object](../reference.md#type-object) | true | — | If specified the callback will be evaluated in the scope of this object - the `this` keyword will be a pointer to this target when the callback is fired. |

### Returns

`[Any](#type-any)` — returns the value returned by the callback method passed in.

---
## ClassMethod: Class.modifyFrameworkDone

### Description
Notifies the SmartClient Class system that the developer is done making changes to the SmartClient framework (as originally indicated by a call to [Class.modifyFrameworkStart](#classmethod-classmodifyframeworkstart)).

New classes created or changes made to existing classes after this method call will be considered application code. This ensures that [Class.isFrameworkClass](#classattr-classisframeworkclass) will not be set to true on Classes defined after this method call.

---
## ClassMethod: Class.setLogPriority

### Description
Set the priority of messages that will be visible for some log category, when logged on this Class or Instance object.  
If called with no category, this priority will be applied to every logged message on this object  
To set the visible log priority for some category across the entire page, use `isc.Log.setPriority()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category for which the log priority will be updated. If not all logs on this canvas will be logged at the priority passed in. |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |

### See Also

- [Log.setPriority](Log.md#classmethod-logsetpriority)

---
## ClassMethod: Class.addMethods

### Description
Helper method for adding method definitions to all instances of this class.

The added methods can be called as myInstance.method().

Functionally equivalent to [Class.addProperties](#method-classaddproperties), which works with both properties and methods.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Object](../reference.md#type-object) | true | — | objects with methods to add (think named parameters). all the methods of each argument will be applied as instance-level methods. |

### Returns

`[Object](../reference.md#type-object)` — the class after methods have been added to it

---
## ClassMethod: Class.logWarn

### Description
Log a message at "warn" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## ClassMethod: Class.Super

### Description
Call the SuperClass implementation of a class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [String](#type-string) | false | — | name of the superclass method to call |
| args | [Arguments](#type-arguments)|[Array](#type-array) | false | — | native "arguments" object, or array of arguments to pass to the Super call |
| nativeArgs | [Arguments](#type-arguments) | true | — | native "arguments" object, required if an Array is passed for the "args" parameter in lieu of the native arguments object |

### Returns

`[Any](#type-any)` — return value of the superclass call

---
## ClassMethod: Class.getCallTrace

### Description
Returns a one-line summary of the current method call, showing method name and passed arguments. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.getCallTrace(arguments)" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

Note the `arguments` object is required in most cases for this method to function. In some browsers, it can be derived automatically, but developers looking to debug on multiple platforms should not rely on this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| args | [Arguments](#type-arguments) | true | — | arguments object from the call to trace. If ommitted, where supported, arguments will be derived from the calling function, or if this is not supported, the method will not function. |

### Groups

- debug

---
## ClassMethod: Class.registerTemplates

### Description
Registers a set of named template functions under a given template type (for example, "default" or "email").

Templates are stored in the class object and prototype inheritance is maintained along the class hierarchy. Subclasses can override templates without mutating their superclass, add new ones, and rely on late binding so templates can be defined at any point.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| templates | [Object](../reference.md#type-object) | false | — | Object mapping template names to template functions. |
| type | [String](#type-string) | true | — | The namespace type for the templates. Defaults to "default". |

### Groups

- stringTemplateFunctions

### See Also

- [stringTemplateFunctions](../kb_topics/stringTemplateFunctions.md#kb-topic-string-template-functions)

---
## ClassMethod: Class.setDefaultLogPriority

### Description
Set the default priority of logging for messages logged on this Class or Instance object. All categories for which there is no explicit, instance level logging priority set will log at this level on this object.  
To set the default visible log priority across the entire page, use `isc.Log.setDefaultPriority()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category for which the log priority will be updated. If not all logs on this canvas will be logged at the priority passed in. |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |

### See Also

- [Log.setPriority](Log.md#classmethod-logsetpriority)

---
## ClassMethod: Class.echoLeaf

### Description
Return a very short (generally less than 40 characters) string representation of any object, suitable for viewing by a developer for debugging purposes. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echoLeaf" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Class.echo](#method-classecho)

---
## ClassMethod: Class.getInstanceProperty

### Description
Gets a named property from the instance defaults for this object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to return |

---
## ClassMethod: Class.logIsWarnEnabled

### Description
Check whether a message logged at "warn" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## ClassMethod: Class.addPropertyList

### Description
Add default properties to all instances of this class

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array of Object](#type-array-of-object)[] | false | — | array of objects with properties to add |

### Returns

`[Object](../reference.md#type-object)` — the class after properties have been added to it

---
## ClassMethod: Class.logError

### Description
Log a message at "error" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## ClassMethod: Class.markAsFrameworkClass

### Description
Mark this class as a framework class (member of the SmartClient framework). Sets [Class.isFrameworkClass](#classattr-classisframeworkclass). May be used in debugging and by the AutoTest subsystem

### Groups

- autoTest

---
## ClassMethod: Class.render

### Description
Renders a template by name from the "default" template namespace type.

Shared template utilities (`sc` and `json`) are automatically initialized and passed in. The template executes with `this` bound to the class object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| templateName | [String](#type-string) | false | — | The name of the template to render, from the "default" namespace type. |
| state | [Object](../reference.md#type-object) | false | — | Input state passed to the template function. |

### Returns

`[String](#type-string)` — Rendered string output, or an empty string if the template function was not found, or an exception occurred during execution of the template function.

### Groups

- stringTemplateFunctions

### See Also

- [stringTemplateFunctions](../kb_topics/stringTemplateFunctions.md#kb-topic-string-template-functions)

---
## ClassMethod: Class.evaluate

### Description
Evaluate a string of script and return the result.

This method is a wrapper around the native javascript method `eval()`. It papers over some native issues to ensure evaluation of script behaves consistently across browsers

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| expression | [String](#type-string) | false | — | the expression to be evaluated |
| evalArgs | [Object](../reference.md#type-object) | false | — | Optional mapping of argument names to values - each key will be available as a local variable when the script is executed. |

### Returns

`[Any](#type-any)` — the result of the eval

---
## ClassMethod: Class.getSuperClass

### Description
Gets a pointer to the superClass' Class object.

### Returns

`[Class](#type-class)` — Class object for superclass.

---
## ClassMethod: Class.setInstanceProperty

### Description
Sets a named property from the instance defaults for this object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| property | [String](#type-string) | false | — | name of the property to return |
| value | [Any](#type-any) | false | — | value to set to |

---
## ClassMethod: Class.isA

### Description
Returns whether this class object is the provided class or is a subclass of the provided class, or implements the provided interface.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | Class name to test against |

### Returns

`[boolean](../reference.md#type-boolean)` — true == this Class is a subclass of the provided classname

---
## ClassMethod: Class.toString

### Description
The default toString() for a ClassObject reports that you have a ClassObject and what class it is.

---
## ClassMethod: Class.create

### Description
Create an instance of this class.

All arguments passed to this method are passed on to the [Class.init](#method-classinit) instance method. Unless [Class.addPropertiesOnCreate](#attr-classaddpropertiesoncreate) is set to `false`, all arguments passed to this method must be Objects and all properties on those objects will be copied to the newly created instance before [Class.init](#method-classinit) is called. If there are overlapping properties in the passed arguments, the last wins.

Any return value from [Class.init](#method-classinit) is thrown away.

Note: Generally, you would not override this method. If you want to specify a constructor for your class, provide an override for [Class.init](#method-classinit) for generic classes or [Canvas.initWidget](Canvas.md#method-canvasinitwidget) for any subclasses of UI components (i.e. descendants of [Canvas](Canvas.md#class-canvas)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Any](#type-any) | true | — | Any arguments passed will be passed along to the init() routine of the instance. Unless [Class.addPropertiesOnCreate](#attr-classaddpropertiesoncreate) is set to false, any arguments passed to this method must be of type Object. |

### Returns

`[Object](../reference.md#type-object)` — New instance of this class, whose init() routine has already been called

---
## ClassMethod: Class.logIsInfoEnabled

### Description
Check whether a message logged at "info" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## ClassMethod: Class.setProperties

### Description
Apply a set of properties to a class object, calling the appropriate setter class methods if any are found.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Object](../reference.md#type-object) | true | — | objects with properties to add (think named parameters). all the properties of each argument will be applied one after another so later properties will override |

---
## ClassMethod: Class.registerStringMethods

### Description
Register a method, or set of methods, that can be provided to instances of this class as Strings (containing a JavaScript expression) and will be automatically converted into functions.

For example:

```
  isc.MyClass.registerStringMethods({
      myStringMethod: "arg1, arg2"
  });
  
```
Note that registered stringMethods are eligible as target methods for `Action`s declared in Component XML files. See the _**Declarative Actions**_ section of the [Component XML article](../kb_topics/componentXML.md#kb-topic-component-xml).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [Object](../reference.md#type-object) | false | — | If this is a string, name of the property to register If this is an object, assume passing in a set of name/value pairs to register |
| argumentString | [String](#type-string) | false | — | named arguments for the property in a comma separated string (not used if methodName is an object) |

### See Also

- [stringMethods](../kb_topics/stringMethods.md#kb-topic-string-methods-overview)

---
## ClassMethod: Class.clearLogPriority

### Description
Clear this object's priority setting for a particular category, so that the category's effective priority returns to the specified priority for this category at the Log level (or `Log.defaultPriority` if not set).  
To clear the Page-level priority setting for this log category use `isc.Log.clearPriority()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category name. If not specified, all logging on this object will revert to default priority settings. |

### See Also

- [Log.clearPriority](Log.md#classmethod-logclearpriority)

---
## ClassMethod: Class.addProperties

### Description
Add default properties and methods to all instances of this class.  
  
These properties can then be accessed as `myInstance.property`, and methods can be called via `myInstance.methodName()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Object](../reference.md#type-object) | true | — | objects with properties to add (think named parameters). all the properties of each argument will be applied |

### Returns

`[Object](../reference.md#type-object)` — the class after properties have been added to it

### See Also

- [Class.addProperties](#method-classaddproperties)
- [isc.addProperties](isc.md#staticmethod-iscaddproperties)

---
## ClassMethod: Class.isMethodSupported

### Description
Returns true if the method is supported by this class, meaning that it is not null and was not replaced by [Class.markUnsupportedMethods](#classmethod-classmarkunsupportedmethods).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [Identifier](../reference.md#type-identifier) | false | — | the name of a method to test. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the method is not null and is not an unsupported method; false otherwise.

**Flags**: A

---
## ClassMethod: Class.logInfo

### Description
Log a message at "info" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## ClassMethod: Class.echo

### Description
Return a short string representation of any object, suitable for viewing by a developer for debugging purposes.

If passed an object containing other objects, echo will not recurse into subobjects, summarizing them instead via echoLeaf().

NOTE: echo() is used to generate the output shown in the Log window when evaluating an expression.

This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echo()" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Log.echoAll](Log.md#classmethod-logechoall)
- [Log.echoLeaf](Log.md#classmethod-logecholeaf)

---
## ClassMethod: Class.map

### Description
Call `method` on each item in `argsList` and return the Array of results.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [String](#type-string) | false | — | Name of the method on this instance which should be called on each element of the Array |
| items | [Array](#type-array) | false | — | Array of items to call the method on |

### Returns

`[Array](#type-array)` — Array of results, one per element in the passed "items" Array

---
## ClassMethod: Class.logDebug

### Description
Log a message at "debug" priority

A method named log_Priority_ exists for each priority level, on every ISC Class and instance of an ISC Class. Messages logged on a Class or instance have a default category of the classname. Messages logged on an instance will also automatically incorporate the instance ID. General best practice is to call logDebug() et al as "this.logDebug" whenever "this" is an instance, or as "Log.logDebug" otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.echo](Log.md#classmethod-logecho)
- [Log.setPriority](Log.md#classmethod-logsetpriority)

---
## ClassMethod: Class.getStackTrace

### Description
Returns a "stack trace" - one line per method in the current call stack, showing the method name and any parameters passed. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.getStackTrace" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

Platform Notes: In Mozilla Firefox, if Firebug is enabled, a stack trace will be logged to the firebug console in addition to the standard stack trace string returned by this method.  
In browsers other than Internet Explorer a complete stack trace may not be available - this occurs when a function is re-entrant (meaning it calls itself). In this case the stack will terminate with text indicating where the recursive function call occurred.

See [debugging](../kb_topics/debugging.md#kb-topic-debugging) for further information information.

### Returns

`[String](#type-string)` — stack trace. Use eg [Class.logWarn](#method-classlogwarn) to log to the Developer Console.

### Groups

- debug

---
## ClassMethod: Class.delayCall

### Description
This is a helper to delay a call to a method on some target by a specified amount of time. Can be used to delay a call to a static method on this class by omitting the `target` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [String](#type-string) | false | — | name of the method to call |
| arrayArgs | [Array](#type-array) | true | — | array of arguments to pass to the method in question |
| time | [number](#type-number) | true | — | Number of ms to delay the call by - defaults to zero (so just pulls execution of the method out of the current execution thread. |
| target | [Object](../reference.md#type-object) | true | — | Target to fire the method on - if unspecified assume this is a call to a classMethod on this Class. |

### Returns

`[String](#type-string)` — Timer ID for the delayed call - can be passed to [Timer.clear](Timer.md#classmethod-timerclear) to cancel the call before it executes

---
## ClassMethod: Class.echoAll

### Description
Like echo(), except that if passed an Array, echoAll() will echo() every element of the Array. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echo()" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Class.echo](#method-classecho)

---
## ClassMethod: Class.modifyFrameworkStart

### Description
Notifies the SmartClient Class system that any new classes created, or changes made to existing classes should be treated as part of the framework. This ensures that [Class.isFrameworkClass](#classattr-classisframeworkclass) will be set to true on any classes defined after this method call, until [Class.modifyFrameworkDone](#classmethod-classmodifyframeworkdone) is called.

Developers may call this method before applying changes which should be considered part of the core framework, rather than application code, for example in _load\_skin.js_ files. When changes are complete, [Class.modifyFrameworkDone](#classmethod-classmodifyframeworkdone) should be called. Note that this is an alternative approach to calling [Class.markAsFrameworkClass](#classmethod-classmarkasframeworkclass) directly on specific classes.

---
## ClassMethod: Class.logFatal

### Description
Log a message at "fatal" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## ClassMethod: Class.markUnsupportedMethods

### Description
Replaces each of the methods named in `methodNames` with a new implementation that simply logs a warning the first time the method is called, and nothing else. This can be used to mark methods of derived classes which do not support certain parent class methods as unsupported.

The `messageTemplate` parameter is a template for the warning message logged when the unsupported method is first called. The following variables in the template are substituted as follows:

| Variable | Substitution |
|---|---|
| $class | The [class name](#method-classgetclassname). |
| $method | The name of the method. |

If you want the literal string of a substitution variable to appear in the warning message, you can escape it by prefixing with a dollar sign. For example, to include "$class" in the warning message, use "$$class" in the template.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messageTemplate | [String](#type-string) | false | — | template for the warning message logged when first called. If null, the default template string "$class does not support the $method() method." is used. |
| methodNames | [Array of Identifier](#type-array-of-identifier) | false | — | the method names to mark as unsupported. |

### See Also

- [Class.isMethodSupported](#classmethod-classismethodsupported)

**Flags**: A

---
## ClassMethod: Class.logIsEnabledFor

### Description
Check whether a message logged at the given priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |
| category | [String](#type-string) | true | — | category to log in |

---
## ClassMethod: Class.addClassProperties

### Description
Add static (Class-level) properties and methods to this object  
  
These properties can then be accessed as MyClass.property, or for functions, called as MyClass.methodName()

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Object](../reference.md#type-object) | true | — | objects with properties to add (think named parameters). all the properties of each argument will be applied as class-level properties. |

### Returns

`[Object](../reference.md#type-object)` — the class after properties have been added to it

---
## ClassMethod: Class.getTemplate

### Description
Retrieves a registered template function by name and type.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | The template name to look up. |
| type | [String](#type-string) | true | — | The namespace type (defaults to "default"). |

### Returns

`[Function](#type-function)` — The registered template function, or `null` if not found.

### Groups

- stringTemplateFunctions

### See Also

- [stringTemplateFunctions](../kb_topics/stringTemplateFunctions.md#kb-topic-string-template-functions)

---
## ClassMethod: Class.getClassName

### Description
Gets the name of this class as a string.

### Returns

`[String](#type-string)` — name of the class

---
## ClassMethod: Class.getDefaultLogPriority

### Description
Retrieves the default priority of messages for this class or instance.

### Returns

`[LogPriority](../reference.md#type-logpriority)` — default priority for logging messages on this object.

---
## ClassMethod: Class.logIsDebugEnabled

### Description
Check whether a message logged at "debug" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## ClassMethod: Class.logIsErrorEnabled

### Description
Check whether a message logged at "error" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## Method: Class.getClassName

### Description
Gets the name of this class as a string.

### Returns

`[String](#type-string)` — String name of this instance's Class object.

---
## Method: Class.getCallTrace

### Description
Returns a one-line summary of the current method call, showing method name and passed arguments. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.getCallTrace(arguments)" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

Note the `arguments` object is required in most cases for this method to function. In some browsers, it can be derived automatically, but developers looking to debug on multiple platforms should not rely on this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| args | [Arguments](#type-arguments) | true | — | arguments object from the call to trace. If ommitted, where supported, arguments will be derived from the calling function, or if this is not supported, the method will not function. |

### Groups

- debug

---
## Method: Class.hasDynamicProperty

### Description
Returns true if the property is dynamic.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [Identifier](../reference.md#type-identifier) | false | — | name of a settable property on this instance |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the property is dynamic

---
## Method: Class.Super

### Description
Call the SuperClass implementation of an instance method. For example:
```
    isc.defineClass("MyButton", "Button").addProperties({
        // this override causes no change in behavior because it just 
        // calls Super and returns whatever the superclass would return
        getTitle : function () {
            return this.Super("getTitle", arguments);
        },

        // this override would add "foo" to the titles of all buttons
        getTitle : function () {
            // add code here to take actions before the superclass method is invoked

            var superResult = return this.Super("getTitle", arguments);

            // add code here to take action after the superclass method is invoked

            return superResult + "foo";
        }

    })
 
```
Note that Super() is always called with the name of the current method. You cannot call the Super class implementation of another method directly.

It is **required** to always pass the native 'arguments' object to Super(). Arguments is a JavaScript builtin that is available within any JavaScript function - see any JavaScript Reference for details.

If you override a method in an instance, and then call Super(), the prototype implementation will be called. This is similar to how anonymous classes in Java handle super(). For example:

```
    isc.Button.create({
        // this will set the title to indicate the runtime button class
        initWidget : function () {
            this.Super("initWidget", arguments);
            this.title = "Parent Class: " + this.getSuperClass().getClassName();
        },
        width: 1,
        overflow: "visible"
    });
 
```
See also [defineClass()](ClassFactory.md#classmethod-classfactorydefineclass) and [addProperties](#classmethod-classaddproperties) for the basics of creating classes and overriding methods.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [String](#type-string) | false | — | name of the superclass method to call |
| args | [Arguments](#type-arguments)|[Array](#type-array) | false | — | native "arguments" object, or array of arguments to pass to the Super call |
| nativeArgs | [Arguments](#type-arguments) | true | — | native "arguments" object, required if an Array is passed for the "args" parameter in lieu of the native arguments object |

### Returns

`[Any](#type-any)` — return value of the superclass call

---
## Method: Class.clearDynamicProperty

### Description
Clears a dynamic property previously established via [Class.addDynamicProperty](#method-classadddynamicproperty).

If the property is not currently dynamic, nothing will be done (and no warning logged).

The current value of the property will not be changed by this call.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [Identifier](../reference.md#type-identifier) | false | — | property name of the dynamic property to clear |

---
## Method: Class.ignore

### Description
Stop observing a method on some other object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to observe |
| methodName | [String](#type-string) | false | — | name of the method to ignore |

### Returns

`[boolean](../reference.md#type-boolean)` — true == observation stopped, false == no change made

### Groups

- observation

### See Also

- [Class.observe](#method-classobserve)

**Flags**: A

---
## Method: Class.logIsDebugEnabled

### Description
Check whether a message logged at "debug" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## Method: Class.logError

### Description
Log a message at "error" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## Method: Class.echoAll

### Description
Like echo(), except that if passed an Array, echoAll() will echo() every element of the Array. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echo()" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Class.echo](#method-classecho)

---
## Method: Class.init

### Description
Initialize a new instance of this Class. This method is called automatically by [Class.create](#classmethod-classcreate).

Override this method to provide initialization logic for your class. If your class is a subclass of a UI component (i.e. descendant of [Canvas](Canvas.md#class-canvas)), override [Canvas.initWidget](Canvas.md#method-canvasinitwidget) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Any](#type-any) | true | — | All arguments initially passed to [Class.create](#classmethod-classcreate) |

**Flags**: A

---
## Method: Class.logIsInfoEnabled

### Description
Check whether a message logged at "info" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## Method: Class.getStackTrace

### Description
Returns a "stack trace" - one line per method in the current call stack, showing the method name and any parameters passed. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.getStackTrace" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

Platform Notes: In Mozilla Firefox, if Firebug is enabled, a stack trace will be logged to the firebug console in addition to the standard stack trace string returned by this method.  
In browsers other than Internet Explorer a complete stack trace may not be available - this occurs when a function is re-entrant (meaning it calls itself). In this case the stack will terminate with text indicating where the recursive function call occurred.

See [debugging](../kb_topics/debugging.md#kb-topic-debugging) for further information information.

### Returns

`[String](#type-string)` — stack trace. Use eg [Class.logWarn](#method-classlogwarn) to log to the Developer Console.

### Groups

- debug

---
## Method: Class.addPropertyList

### Description
Add properties to this instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| list | [Array of Object](#type-array-of-object)[] | false | — | array of objects with properties to add |

### Returns

`[Object](../reference.md#type-object)` — the object after properties have been added to it

---
## Method: Class.isObserving

### Description
Return true if this object is already observing a method of another object

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object we may be observing |
| methodName | [String](#type-string) | false | — | name of the method to observed |

### Returns

`[boolean](../reference.md#type-boolean)` — true if we're already observing that method

### Groups

- observation

**Flags**: A

---
## Method: Class.getSuperClass

### Description
Gets a pointer to the class object for this instance's superclass.

### Returns

`[Class](#type-class)` — Class object for superclass.

---
## Method: Class.logIsWarnEnabled

### Description
Check whether a message logged at "warn" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## Method: Class.delayCall

### Description
This is a helper to delay a call to some method on this object by some specified amount of time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [String](#type-string) | false | — | name of the method to call |
| arrayArgs | [Array](#type-array) | true | — | array of arguments to pass to the method in question |
| time | [number](#type-number) | true | — | Number of ms to delay the call by - defaults to zero (so just pulls execution of the method out of the current execution thread. |

### Returns

`[String](#type-string)` — Timer ID for the delayed call - can be passed to [Timer.clear](Timer.md#classmethod-timerclear) to cancel the call before it executes

---
## Method: Class.addAutoChild

### Description
Creates a component according to the "AutoChild" pattern, and adds it to this component.

See the [AutoChild usage overview](../kb_topics/autoChildren.md#kb-topic-autochildren) to understand the general purpose and usage of this method.

`addAutoChild()` takes the following actions:

1.  checks whether this._autoChildName_ is already populated, and returns it if so
2.  checks when there is a show_AutoChildName_ with the value false, and if so returns without creating a component
3.  calls [Class.createAutoChild](#method-classcreateautochild) to create the component
4.  sets this._autoChildName_ to the created component
5.  adds the component either to this component, or to some other parent, specified by the "autoParent" property in the autoChild's defaults. The "autoParent" property may be "none" indicating the autoChild should not be automatically added.

When adding an autoChild to a [Layout](Layout.md#class-layout) subclass, [addMember()](Layout.md#method-layoutaddmember) will be called instead of the normal [addChild()](Canvas.md#method-canvasaddchild). To prevent this behavior, `addAsChild:true` can be set in the autoChild defaults. Similarly, `addAsPeer:true` may be set to add an autoChild as a peer.

**Tip:** because `addAutoChild()` checks specifically for show_AutoChildName_:false, you do not have to add show_AutoChildName_:true in order for an autoChild to be shown by default; leaving the property undefined is sufficient.

Note that by default the child created by this method will be destroyed when [destroy()](Canvas.md#method-canvasdestroy) is called on this instance. To disable this behavior, set `dontAutoDestroy` to true on the auto child.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| childName | [String](#type-string) | false | — | name of the autoChild |
| defaults | [Properties](../reference.md#type-properties) | false | — | dynamic properties for the autoChild |

### Returns

`[Class](#type-class)` — created autoChild

### Groups

- autoChildren

---
## Method: Class.isA

### Description
Returns whether this object is of a particular class by class name, either as a direct instance of that class or as subclass of that class, or by implementing an interface that has been mixed into the class.  
  
NOTE: this only applies to ISC's class system, eg: `myInstance.isA("Object")` will be false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| className | [String](#type-string) | false | — | Class name to test against |

### Returns

`[boolean](../reference.md#type-boolean)` — whether this object is of that Class or a subClass of that Class

---
## Method: Class.setProperties

### Description
Set multiple properties on an object, calling the appropriate setter methods if any are found.

Whenever you set a property on an ISC component, you should call either the specific setter for that property, or `setProperty()/setProperties()` if it doesn't have one. This future-proofs your code against the later addition of required setters.

With `setProperties()` in particular, some classes may be able to take shortcuts and be more efficient when 2 or more related properties are set at the same time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Object](../reference.md#type-object) | true | — | objects with properties to add (think named parameters). all the properties of each argument will be applied one after another so later properties will override |

### See Also

- [Class.setProperty](#method-classsetproperty)

---
## Method: Class.getClass

### Description
Gets a pointer to the class object for this instance

### Returns

`[Class](#type-class)` — Class object that was used to construct this object

---
## Method: Class.setLogPriority

### Description
Set the priority of messages that will be visible for some log category, when logged on this Class or Instance object.  
If called with no category, this priority will be applied to every logged message on this object  
To set the visible log priority for some category across the entire page, use `isc.Log.setPriority()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category for which the log priority will be updated. If not all logs on this canvas will be logged at the priority passed in. |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |

### See Also

- [Log.setPriority](Log.md#classmethod-logsetpriority)

---
## Method: Class.createAutoChild

### Description
Unconditionally creates and returns a component created according to the "AutoChild" pattern.

In addition to applying defaults and properties as described under the [AutoChild overview](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren), the created autoChild:

*   is automatically `autoDraw:false`
*   has a `creator` property that points to this component, for easy authoring of event handlers (eg click:"this.creator.doSomething()")

Unlike [Class.addAutoChild](#method-classaddautochild), `createAutoChild()` does not create a this._autoChildName_ reference to the component, check a show_AutoChildName_ flag, or automatically add the autoChild via [Canvas.addChild](Canvas.md#method-canvasaddchild).

General you use `createAutoChild` rather than addAutoChild when:

*   you are going to create several autoChildren with a common set of defaults (for example the [column](ColumnTree.md#attr-columntreecolumn) autoChild of the [ColumnTree](ColumnTree.md#class-columntree)).
*   children need to be created before their parents (eg, for layout/auto-sizing reasons)

Note that by default the child created by this method will be destroyed when [destroy()](Canvas.md#method-canvasdestroy) is called on this instance. To disable this behavior, set `dontAutoDestroy` to true on the auto child.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| childName | [String](#type-string) | false | — | name of the autoChild |
| defaults | [Properties](../reference.md#type-properties) | false | — | dynamic properties for the autoChild |

### Returns

`[Class](#type-class)` — created autoChild

### Groups

- autoChildren

---
## Method: Class.logDebug

### Description
Log a message at "debug" priority

A method named log_Priority_ exists for each priority level, on every ISC Class and instance of an ISC Class. Messages logged on a Class or instance have a default category of the classname. Messages logged on an instance will also automatically incorporate the instance ID. General best practice is to call logDebug() et al as "this.logDebug" whenever "this" is an instance, or as "Log.logDebug" otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.echo](Log.md#classmethod-logecho)
- [Log.setPriority](Log.md#classmethod-logsetpriority)

---
## Method: Class.destroy

### Description
Permanently destroy a class instance and any automatically created resources, recursively.

### See Also

- [Canvas.destroy](Canvas.md#method-canvasdestroy)
- [memoryLeaks](../kb_topics/memoryLeaks.md#kb-topic-memory-leaks)

**Flags**: A

---
## Method: Class.clearLogPriority

### Description
Clear this object's priority setting for a particular category, so that the category's effective priority returns to the specified priority for this category at the Log level (or `Log.defaultPriority` if not set).  
To clear the Page-level priority setting for this log category use `isc.Log.clearPriority()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category name. If not specified, all logging on this object will revert to default priority settings. |

### See Also

- [Log.clearPriority](Log.md#classmethod-logclearpriority)

---
## Method: Class.getDynamicPropertyRuleTime

### Description
Returns the last time the rule for the specified dynamic property fired, as a [Date](../reference_2.md#object-date).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [Identifier](../reference.md#type-identifier) | false | — | name of a settable property on this instance |

### Returns

`[Date](#type-date)` — last fire time of rule

---
## Method: Class.logIsEnabledFor

### Description
Check whether a message logged at the given priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |
| category | [String](#type-string) | true | — | category to log in |

---
## Method: Class.setDefaultLogPriority

### Description
Set the default priority of logging for messages logged on this Class or Instance object. All categories for which there is no explicit, instance level logging priority set will log at this level on this object.  
To set the default visible log priority across the entire page, use `isc.Log.setDefaultPriority()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category for which the log priority will be updated. If not all logs on this canvas will be logged at the priority passed in. |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |

### See Also

- [Log.setPriority](Log.md#classmethod-logsetpriority)

---
## Method: Class.setProperty

### Description
Set a property on this object, calling the setter method if it exists.

Whenever you set a property on an ISC component, you should call either the specific setter for that property, or `setProperty()/setProperties()` if it doesn't have one. This future-proofs your code against the later addition of required setters.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string) | false | — | name of the property to set |
| newValue | [Any](#type-any) | false | — | new value for the property |

### See Also

- [Class.setProperties](#method-classsetproperties)

---
## Method: Class.logIsErrorEnabled

### Description
Check whether a message logged at "error" priority would be visible in the log.

As with logDebug, category is defaulted to the current className. Use this method to avoid putting together expensive log messages if they will never appear in the log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | true | — | category to log in |

---
## Method: Class.echo

### Description
Return a short string representation of any object, suitable for viewing by a developer for debugging purposes.

If passed an object containing other objects, echo will not recurse into subobjects, summarizing them instead via echoLeaf().

NOTE: echo() is used to generate the output shown in the Log window when evaluating an expression.

This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echo()" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Log.echoAll](Log.md#classmethod-logechoall)
- [Log.echoLeaf](Log.md#classmethod-logecholeaf)

---
## Method: Class.addDynamicProperty

### Description
Sets up the value of `propertyName` to be dynamically derived from the [ruleScope](Canvas.md#attr-canvasrulescope), by either a simple [DataPath](../reference_2.md#type-datapath) into the ruleScope, an [AdvancedCriteria](../reference.md#object-advancedcriteria) built against [DataPaths](../reference_2.md#type-datapath), or via a textual or numeric formula using the ruleScope as available formula inputs.

The dataPath, criteria, or formula is evaluated immediately when addDynamicProperty() is called, then re-evaluated every time the ruleScope changes. An [AdvancedCriteria](../reference.md#object-advancedcriteria) will always evaluate to boolean true or false, and a [UserSummary](../reference.md#object-usersummary) to a string.

It is invalid usage to use `addDynamicProperty()` on a property that is not runtime settable. However, `addDynamicProperty()` will not throw an error or log a warning if this is done.

If a property is already dynamic and addDynamicProperty() is called again, the new dynamic behavior replaces the old. If a property should no longer be dynamic, call [Class.clearDynamicProperty](#method-classcleardynamicproperty).

Dynamic properties can also be declared together via [Class.dynamicProperties](#attr-classdynamicproperties).

Note that you may convert a simple criteria to an [AdvancedCriteria](../reference.md#object-advancedcriteria) by calling [DataSource.convertCriteria](DataSource.md#classmethod-datasourceconvertcriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [Identifier](../reference.md#type-identifier) | false | — | name of a settable property on this instance |
| source | [DataPath](../reference_2.md#type-datapath)|[UserSummary](#type-usersummary)|[UserFormula](#type-userformula)|[AdvancedCriteria](#type-advancedcriteria) | false | — | — |

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [Class.dynamicProperties](#attr-classdynamicproperties)

---
## Method: Class.logInfo

### Description
Log a message at "info" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## Method: Class.getID

### Description
Return the global identifier for this object.

### Returns

`[String](#type-string)` — global identifier for this canvas

---
## Method: Class.logWarn

### Description
Log a message at "warn" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## Method: Class.getDefaultLogPriority

### Description
Retrieves the default priority of messages for this class or instance.

### Returns

`[LogPriority](../reference.md#type-logpriority)` — default priority for logging messages on this object.

---
## Method: Class.echoLeaf

### Description
Return a very short (generally less than 40 characters) string representation of any object, suitable for viewing by a developer for debugging purposes. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echoLeaf" whenever "this" is an instance, or call the static classMethod on the [Log](Log.md#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Class.echo](#method-classecho)

---
## Method: Class.addProperties

### Description
Add properties or methods to this specific instance. Properties with the same name as existing properties will override.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Object](../reference.md#type-object) | true | — | Object containing name:value pairs to be added to this object |

### Returns

`[Object](../reference.md#type-object)` — the object after properties have been added to it

### See Also

- [Class.addProperties](#classmethod-classaddproperties)
- [isc.addProperties](isc.md#staticmethod-iscaddproperties)

---
## Method: Class.fireCallback

### Description
Method to fire a callback. Callback will be fired in the scope of the object on which this method is called.  
Falls through to [Class.fireCallback](#classmethod-classfirecallback)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | Callback to fire |
| argNames | [String](#type-string) | true | — | comma separated string of variables |
| args | [Array](#type-array) | true | — | array of arguments to pass to the method |

### Returns

`[Any](#type-any)` — returns the value returned by the callback method passed in.

---
## Method: Class.toString

### Description
The default toString() for instances reports that you have an instance of a class and prints the instance ID if present.

---
## Method: Class.observe

### Description
Set up a notification action to be invoked whenever some method is called on a target object.

For example, if you wanted to take an action every time some ListGrid on your page had its [selection updated](ListGrid_2.md#method-listgridselectionupdated), instead of _overriding_ the `selectionUpdated()` method on the grid, you could observe it with code like this:

`myCanvas.observe(myListGrid, "selectionUpdated", "observer.gridSelectionUpdated()")`

In this example, every time _selectionUpdated()_ fired on the grid "myListGrid", after that method completed, the specified action would be invoked. (In this case the action would call a method called "gridSelectionUpdated" on the observer, "myCanvas").

An unlimited number of observers can be set up to observe any method. The notification actions will all be fired automatically in the order that the observations were set up.

NOTES:

*   The object to observe may be any JavaScript object with the specified method, including simple JavaScript Objects or Arrays, or instances of SmartClient classes like [Canvas](Canvas.md#class-canvas).
*   For a given observer, observed object, and observed method combination, at most one action can be registered. If you attempt to call `observe()` again with the same combination, it will return false and the action will not be registered.
*   A method could potentially trigger an observation of itself by another object, either through code within the method itself or within an observer's action.  
    In this case the observation will be set up, but the new observation action will not fire as part of this thread. For subsequent calls to the method, the newly added observer will be fired.
*   _\[Potential memory leak\]_: If the target object is a simple JavaScript object (not an instance of a SmartClient class), developers should always call [ignore()](#method-classignore) to stop observing the object when an observation is no longer necessary.  
    This ensures that if the observed object is subsequently allowed to go out of scope by application code, the observation system will not retain a reference to it (so the browser can reclaim the allocated memory).  
    While cleaning up observations that are no longer required is always good practice, this memory leak concern is not an issue if the target object is an instance of a SmartClient class. In that case the observation is automatically released when the target is [destroyed](#method-classdestroy).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to observe. This may be any JavaScript object with the specified target method, including native arrays, and instances of SmartClient classes such as [Canvas](Canvas.md#class-canvas). |
| methodName | [String](#type-string) | false | — | Name of the method to observe. Every time this method is invoked on the target object the specified action will fire (after the default implementation completes). |
| action | [Function](#type-function)|[String](#type-string) | true | — | Optional action to take when the observed method is invoked on the target object.  
If `action` is a string to execute, certain keywords are available for context:

*   `observer` is this object (the object on which the `observe(...)` method was called).
*   `observed` is the target object being observed (on which the method was invoked).
*   `returnVal` is the return value from the observed method (if there is one)
*   For functions defined with explicit parameters, these will also be available as keywords within the action string

If `action` is a function, this will be executed in the scope of the observer (so `this` will be the object on which `observe()` was invoked). The arguments for the original method will also be passed to this action function as arguments. If developers need to access the target object being observed from the action function they may use native javascript techniques such as [javascript closure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) to do so. The return value from the observed method is not available to the action function.  
If the `action` parameter is omitted the default behavior will invoke the same named method on the observer, passing in the same parameters. |

### Returns

`[boolean](../reference.md#type-boolean)` — true == observation set up, false == observation not set up

### Groups

- observation

### See Also

- [Class.ignore](#method-classignore)

---
## Method: Class.logFatal

### Description
Log a message at "fatal" priority

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](Log.md#classmethod-loglogdebug)

---
## Method: Class.evaluate

### Description
Evaluate a string of script in the scope of this instance (so `this` is available as a pointer to the instance).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| expression | [String](#type-string) | false | — | the expression to be evaluated |
| evalArgs | [Object](../reference.md#type-object) | false | — | Optional mapping of argument names to values - each key will be available as a local variable when the script is executed. |

### Returns

`[Any](#type-any)` — the result of the eval

### See Also

- [Class.evaluate](#classmethod-classevaluate)

---
## Method: Class.map

### Description
Call `method` on each item in `argsList` and return the Array of results.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| methodName | [String](#type-string) | false | — | Name of the method on this instance which should be called on each element of the Array |
| items | [Array](#type-array) | false | — | Array of items to call the method on |

### Returns

`[Array](#type-array)` — Array of results, one per element in the passed "items" Array

---
