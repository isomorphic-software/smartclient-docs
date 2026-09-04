# Validator Documentation

[← Back to API Index](../reference.md)

---

## Class: Validator

### Description
A validator describes a check that should be performed on a value the user is trying to save.

Validators are specified for DataSource fields via the [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators) property and [are executed in the order in which they are defined](../reference.md#kb-topic-validatorexecution). Validators that need not be run on the server can also be specified for a specific [FormItem](FormItem.md#class-formitem) or [ListGridField](../reference.md#object-listgridfield).

SmartClient supports a powerful library of [ValidatorTypes](../reference.md#type-validatortype) which have identical behavior on both the client and the server.

Beyond this, custom validators can be defined on the client and custom validation logic added on the server. Note that the `regexp` and `mask` validator types are very flexible and can be used to perform virtually any kind of formatting check that doesn't involve some large external dataset.

Custom validators can be reused on the client by adding them to the global validator list, via the [Validator.addValidator](#classmethod-validatoraddvalidator) method.

### See Also

- [ValidatorType](../reference.md#type-validatortype)

---
## ClassAttr: Validator.notADate

### Description
Default error message to display when standard `isDate` type validator returns false.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.requiredField

### Description
Default error message to display when validation fails for a field marked as required or with a standard `required` type validator. The message is also displayed for a field with a standard `requiredIf` type validator whose condition evaluates to true, because the field has no value.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeShorterThan

### Description
Default error message to display when standard `lengthRange` type validator returns false because the value passed in has more than `validator.max` characters. This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.DISABLED

### Description
A declared value of the enum type [FieldAppearance](../reference.md#type-fieldappearance).

**Flags**: R

---
## ClassAttr: Validator.mustBeLessThan

### Description
Default error message to display when standard `integerRange` type validator returns false because the value passed in is greater than the specified maximum. This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.HIDDEN

### Description
A declared value of the enum type [FieldAppearance](../reference.md#type-fieldappearance).

**Flags**: R

---
## ClassAttr: Validator.notABoolean

### Description
Default error message to display when standard `isBoolean` type validator returns false.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeGreaterThan

### Description
Default error message to display when standard `integerRange` type validator returns false because the value passed in is less than the specified minimum.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.notAnInteger

### Description
Default error message to display when standard `isInteger` type validator returns false.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeLaterThanTime

### Description
Default error message to display when standard `timeRange` type validator returns false because the time-portion of the date-value passed in is less than the specified minimum time.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeExactLength

### Description
Default error message to display when standard `lengthRange` type validator has `validator.max` and `validator.min` set to the same value, and returns false because the value passed is not the same length as these limits.  
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.notADecimal

### Description
Default error message to display when standard `isFloat` type validator returns false.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeLaterThan

### Description
Default error message to display when standard `dateRange` type validator returns false because the value passed in is greater than the specified maximum date.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.notAString

### Description
Default error message to display when standard `isString` type validator returns false.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeEarlierThan

### Description
Default error message to display when standard `dateRange` type validator returns false because the value passed in is less than the specified maximum date. This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeEarlierThanTime

### Description
Default error message to display when standard `timeRange` type validator returns false because the time-portion of the date-value passed in is greater than the specified minimum time.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.mustBeLongerThan

### Description
Default error message to display when standard `lengthRange` type validator returns false because the value passed in has fewer than `validator.min` characters. This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `max` and `min` available as variables mapped to `validator.max` and `validator.min`.

### Groups

- i18nMessages

**Flags**: IRA

---
## ClassAttr: Validator.maxFileSizeExceeded

### Description
Default error message to display when the standard `maxFileSize` type validator returns `false`.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: Validator.READONLY

### Description
A declared value of the enum type [FieldAppearance](../reference.md#type-fieldappearance).

**Flags**: R

---
## ClassAttr: Validator.notOneOf

### Description
Default error message to display when standard `isOneOf` type validator is not passed.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: Validator.caseSensitive

### Description
Applies only to the "isUnique" and "hasRelatedRecord" validators and controls whether the search for existing records is case sensitive or not.

**Flags**: IR

---
## Attr: Validator.min

### Description
Indicates the minimum value for range-based validators. By default, range-validators are inclusive, meaning that values that equal the `min` value will pass validation. To make a validator-range exclusive, and have equal values fail validation, set [validator.exclusive](#attr-validatorexclusive) to true and provide a [custom message](#attr-validatorerrormessage).

### See Also

- [Validator.max](#attr-validatormax)
- [Validator.exclusive](#attr-validatorexclusive)

**Flags**: IR

---
## Attr: Validator.serverObject

### Description
For validators of type "serverCustom" only, a [ServerObject](../reference_2.md#object-serverobject) declaration that allows the SmartClient Server to find a Java class via a variety of possible approaches, and call a method on it to perform validation.

The target object must implement a method whose first 4 arguments are: `Object value, Validator validator, String fieldName, Map record`

(`com.isomorphic.datasource.Validator` is a subclass of `Map` that represents a validator's configuration, and also provides APIs for implementing templated error messages).

You provide the name of the method to call by specifying [methodName](ServerObject.md#attr-serverobjectmethodname) as part of the serverObject declaration. If you do not specify a methodName, SmartClient expects to find a compliant method called "condition".

Additional arguments may be declared and are automatically supplied based on the declared argument type, via [DMI](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation). Available objects include:

*   **DataSource** - the DataSource where this validator is declared, an instance of com.isomorphic.datasource.DataSource or a subclass
*   **HttpServletRequest** - from standard Java servlets API
*   **HttpServletResponse** - from standard Java servlets API
*   **ServletContext** - from standard Java servlets API
*   **HttpSession** - from standard Java servlets API
*   **RequestContext** - an instance of com.isomorphic.servlet.RequestContext
*   **RPCManager** - the RPCManager associated with the transaction this validation is part of; an instance of com.isomorphic.rpc.RPCManager
*   **DSRequest** - the DSRequest this validation is part of; an instance of com.isomorphic.datasource.DSRequest
*   **DSField** - the datasource field which value is validated; an instance of com.isomorphic.datasource.DSField
*   **ValidationContext** - the context where value is validated; an instance of com.isomorphic.datasource.ValidationContext

Note that any servlet-related objects will not be available if your validator is run outside of the scope of an HTTP servlet request, such as a command-line process.

Note that "record" will contain only other values submitted at the same time, not the complete DataSource record. For most types of cross-field validation, you should fetch the current saved record. For example:

```
     final Map existingRecord = dataSource.fetchById(record);
 
```

**Flags**: IR

---
## Attr: Validator.operationId

### Description
Applies only to the "isUnique" validator; allows you to name a specific [operation](DataSource.md#attr-datasourceoperationbindings) for the uniqueness check.

**Flags**: IR

---
## Attr: Validator.errorMessage

### Description
Text to display if the value does not pass this validation check.

If unspecified, default error messages exist for all built-in validators, and a generic message will be used for a custom validator that is not passed.

Server-side this string evaluates in a Velocity context where the variables $value and $fieldName are available and refer to the supplied value and the field name, respectively. Note that if the validator is intended to run both on the client and server, you shouldn't use these velocity vars as they will not be expanded on the client and the user may then see raw uninterpolated strings.

**Flags**: IR

---
## Attr: Validator.validateOnChange

### Description
If true, validator will be validated when each item's "change" handler is fired as well as when the entire form is submitted or validated. If false, this validator will not fire on the item's "change" handler.

Note that this property can also be set at the form/grid or field level; If true at any level and not explicitly false on the validator, the validator will be fired on change - displaying errors and rejecting the change on validation failure.

**Flags**: IRW

---
## Attr: Validator.dependentFields

### Description
User-defined list of fields on which this validator depends. Primarily used for validators of type "custom" but can also be used to supplement [Validator.applyWhen](#attr-validatorapplywhen) criteria.

Note that for validators run on the server, fields required due to `dependentFields` but not present in the [DSRequest.data](DSRequest.md#attr-dsrequestdata) of an update because they haven't changed will be filled in from the server DataSource.

### See Also

- [Validator.applyWhen](#attr-validatorapplywhen)

**Flags**: IRA

---
## Attr: Validator.stopOnError

### Description
Indicates that if this validator is not passed, the user should not be allowed to exit the field - focus will be forced back into the field until the error is corrected.

This property defaults to [FormItem.stopOnError](FormItem.md#attr-formitemstoponerror) if unset.

Enabling this property also implies [FormItem.validateOnExit](FormItem.md#attr-formitemvalidateonexit) is automatically enabled. If this is a server-based validator, setting this property also implies that [FormItem.synchronousValidation](FormItem.md#attr-formitemsynchronousvalidation) is forced on.

**Flags**: IR

---
## Attr: Validator.max

### Description
Indicates the maximum value for range-based validators. By default, range-validators are inclusive, meaning that values that equal the `max` value will pass validation. To make a validator-range exclusive, and have equal values fail validation, set [validator.exclusive](#attr-validatorexclusive) to true and provide a [custom message](#attr-validatorerrormessage).

### See Also

- [Validator.min](#attr-validatormin)
- [Validator.exclusive](#attr-validatorexclusive)

**Flags**: IR

---
## Attr: Validator.applyWhen

### Description
Used to create a conditional validator based on [criteria](../reference.md#object-advancedcriteria). The criteria defines when the validator applies. The form current values or ListGrid record is used as reference for the criteria. If the criteria match, then the validator will be processed. Otherwise the validator is skipped and assumed valid.

To use an `applyWhen` criteria the form or grid must use a [DataSource](DataSource.md#class-datasource).

**NOTE:** `applyWhen` is not supported for "binary" fields.

#### Server and client use
Conditional validators are enforced both on the server and on the client-side when defined on a DataSource field as shown in the examples below. Note the `applyWhen` element is treated as a [Criterion](../reference.md#object-criterion).
```
 <!-- Normal format -->
 <field name="age" type="integer">
   <validators>
     <validator type="integerRange" min="0" max="100">
       <applyWhen operator="or">
         <criteria>
           <criterion fieldName="restrictAge" operator="equals" value="true"/>
           <criterion fieldName="gender" operator="equals" value="female"/>
         </criteria> 
       </applyWhen>
     </validator>
   </validators>
 </field>

 <!-- Conditional requirement -->
 <field name="reason" type="text">
   <validators>
     <validator type="required">
       <applyWhen fieldName="willAttend" operator="equals" value="false"/>
     </validator>
   </validators>
 </field>
 
```
The last example above shows an alternate to the `requiredIf` validator using a [shorthand format](../reference.md#kb-topic-xmlcriteriashorthand) which is only available for client-side use. On the client the `reason` field will change appearance to match other required or non-required fields when `willAttend` changes. Note that using `applyWhen` for a validator of type `required` as in the example may result in validation request being set to the server where a fetch is made against the DataSource. For more details, see the discussion at the end of the [DataSourceField.required](DataSourceField.md#attr-datasourcefieldrequired) help topic.

#### Component XML and client-only use
Conditional validators can also be applied to [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) similarly to provide client-only validations or read-only state management. A common use case is conditionally displaying or enabling fields. Use the `readOnly` validator with an `applyWhen` value to control the read-only appearance of a field. The example below shows a field which is hidden when `willAttend=true`.
```
 <!-- field definition within a Component XML DynamicForm -->
 <field name="reason" type="text">
   <validators>
     <validator type="readOnly" fieldAppearance="hidden">
       <applyWhen fieldName="willAttend" operator="equals" value="true"/>
     </validator>
   </validators>
 </field>
 
```

Conditional validators can be applied to DynamicForm or ListGrid fields in JavaScript code as well.

**Flags**: IRA

---
## Attr: Validator.serverCondition

### Description
For validators of type "serverCustom" only: a scriptlet in any supported JSR223 scripting language which is run in order to see if validation passes. For example:

```
     <validator type="serverCustom">
         <serverCondition language="groovy"><![CDATA[
             value < dataSources.StockItem.fetchById(record.itemId).quantity
         ]]></serverCondition>
     </validator>
 
```
The scriptlet should return a boolean true or false value - failing to return a value will be considered a false result (validator failed). If your expression is syntactically invalid, an exception is thrown and the error message is displayed in the client.

See [serverScript](../kb_topics/serverScript.md#kb-topic-server-scripting) for general information on Server Scripting and JSR223, and [velocitySupport](#kb-topic-velocitysupport) for general information on Velocity support, and also see below for special rules for Velocity.

**Available variables** The following variables are available in a `serverCondition`:

*   **dataSource** - The current DataSource
*   **record** - Other submitted values part of the same update
*   **value** - The value of the field
*   **validator** - The config of this validator, including all attributes declared on the `<validator>` tag, presented as a `Map`
*   **field** - The field (as a `DSField` object)

Note that "record" will contain only other values submitted at the same time, not the complete DataSource record. For most types of cross-field validation, you should fetch the current saved record using the server-side API DataSource.fetchById(). For example, in Velocity:
```
     $dataSource.fetchById($record.primaryKeyField).otherFieldName
 
```
Note that, while a DSRequest provides dsRequest.oldValues, these values cannot be relied upon for a security check since they could be faked.

Server-side custom validators also have access to the standard set of context variables that come from the Servlet API. However, be aware that if you write conditions that depend upon these variables, you preclude your Validator from being used in the widest possible variety of circumstances; for example, in a command-line process. Rather, it will be tied to operating in the context of, say, an `HttpSession`.

Given the above caveat, the following context variables are also available:

*   **servletRequest** - The associated `HttpServletRequest`
*   **session** - The associated `HttpSession`
*   **httpParameters** - This variable gives you access to the parameters `Map` of the associated `HttpServletRequest`; it is an alternate form of `$servletRequest.getParameter`
*   **requestAttributes** - This variable gives you access to the attributes `Map` of the associated `HttpServletRequest`; it is an alternate form of `$servletRequest.getAttribute`
*   **sessionAttributes** - This variable gives you access to the attributes `Map` of the associated `HttpSession`; it is an alternate form of `$session.getAttribute`

**Special considerations for Velocity**

To return a true or false value in Velocity, you script can either be just an expression that returns a boolean value, or the result of evaluating the Velocity template can result in output of "true" or "false". All of the following are valid forms:

  `$value < 100     $util.contains($value, "some string")     $record.someField`(assuming that "someField" contains a boolean value)  `$value > $record.otherField`

For additional troubleshooting information when Velocity expressions aren't working as expected, set the log category org.apache.Velocity to DEBUG in log4j.isc.config.xml.

Because it's tricky to call arbitrary Java methods in Velocity, the following special objects are passed to Velocity for convenience:

*   **dataSources** - The list of all DataSources, accessible by name (so, for example, `$dataSources.supplyItem` refers to the `supplyItem` DataSource object).
*   **util** - A `com.isomorphic.util.DataTools` object, giving you access to all of that class's useful helper functions

**Flags**: IR

---
## Attr: Validator.resultingValue

### Description
To transform the incoming value that is validated into a different value or format set this property from [Validator.condition](#attr-validatorcondition) to the desired value.

**Flags**: IR

---
## Attr: Validator.stopIfFalse

### Description
Normally, all validators defined for a field will be run [in the order in which they are defined](../reference.md#kb-topic-validatorexecution) even if one of the validators has already failed. However, if `stopIfFalse` is set, validation will not proceed beyond this validator if the check fails.

This is useful to prevent expensive validators from being run unnecessarily, or to allow custom validators that don't need to be robust about handling every conceivable type of value.

**Flags**: IR

---
## Attr: Validator.exclusive

### Description
When set to true, values that equal the specified [Validator.min](#attr-validatormin) or [Validator.max](#attr-validatormax) values will fail validation. When setting this property, consider also adding a [custom message](#attr-validatorerrormessage).

### See Also

- [Validator.min](#attr-validatormin)
- [Validator.max](#attr-validatormax)

**Flags**: IR

---
## Attr: Validator.type

### Description
Type of the validator.

This can be one of the built-in [ValidatorType](../reference.md#type-validatortype), the string "custom" to define a custom validator, or the string "serverCustom" to define a server-only custom validator.

**Flags**: IR

---
## Attr: Validator.serverOnly

### Description
Indicates this validator runs on the server only.

**Flags**: IR

---
## Attr: Validator.clientOnly

### Description
Indicates this validator runs on the client only.

Normally, if the server is trying to run validators and finds a validator that it can't execute, for safety reasons validation is considered to have failed. Use this flag to explicitly mark a validator that only needs to run on the client.

**Flags**: IR

---
## Attr: Validator.condition

### Description
For a validator that is not a built-in [ValidatorType](../reference.md#type-validatortype), a [Callback](../reference.md#type-callback), function, or JavaScript expression to evaluate to see if this validator passes or fails.

Because the validator declaration itself is passed as a parameter to `condition()`, you can effectively parameterize the validator. For example, to create a validator that checks that the value is after a certain date:

```
 
     { type:"custom", afterDate:new Date(), 
       condition:"value.getTime() > validator.afterDate.getTime()" }
 
```
Reusable validators, like the above, can be registered as a standard validatorType by calling [Validator.addValidator](#classmethod-validatoraddvalidator).

Note that, if a field is declared with a builtin [FieldType](../reference.md#type-fieldtype), the value passed in will already have been converted to the specified type, if possible.

For the required parameters, see the documentation for [ValidatorConditionCallback](Callbacks.md#method-callbacksvalidatorconditioncallback).

**Flags**: IR

---
## ClassMethod: Validator.create

### Description
A Validator shouldn't be created directly. Instead pass [Properties](../reference.md#type-properties) as each Validator in [FormItem.validators](FormItem.md#attr-formitemvalidators) or wherever a Validator is needed.

---
## ClassMethod: Validator.addValidatorDefinitions

### Description
Add several new validator types at once, as though [Validator.addValidatorDefinition](#classmethod-validatoraddvalidatordefinition) were called several times.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newDefinitions | [Object](../reference_2.md#type-object) | false | — | Set of validators to add. This parameter should be a JavaScript object where the property names are validator type names, and the property values are [ValidatorDefinition](../reference.md#object-validatordefinition)s. |

### Groups

- validation

### See Also

- [Validator.addValidatorDefinition](#classmethod-validatoraddvalidatordefinition)

**Flags**: A

---
## ClassMethod: Validator.addValidators

### Description
Add several new validator types at once, as though [Validator.addValidator](#classmethod-validatoraddvalidator) were called several times.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValidators | [Object](../reference_2.md#type-object) | false | — | Set of validators to add. This parameter should be a JavaScript object where the property names are validator type names, and the property values are condition functions or expressions, for example:  
   `{type1:condition1, type2:condition2}`  
. |

### Groups

- validation

### See Also

- [Validator.addValidator](#classmethod-validatoraddvalidator)

**Flags**: A

---
## ClassMethod: Validator.addValidatorDefinition

### Description
Add a new validator type that can be specified as [Validator.type](#attr-validatortype) anywhere validators are declared, such as [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators) or [FormItem.validators](FormItem.md#attr-formitemvalidators).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [String](#type-string) | false | — | type name for the new validator |
| definition | [ValidatorDefinition](#type-validatordefinition) | false | — | the validator definition |

### Groups

- validation

### See Also

- [Validator.addValidatorDefinitions](#classmethod-validatoraddvalidatordefinitions)

**Flags**: A

---
## ClassMethod: Validator.addValidator

### Description
Add a new validator type that can be specified as [Validator.type](#attr-validatortype) anywhere validators are declared, such as [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators) or [FormItem.validators](FormItem.md#attr-formitemvalidators).  
The `condition` argument should be a method of the same signature as [Validator.condition](#attr-validatorcondition).

This method is essentially a shortcut for building a [ValidatorDefinition](../reference.md#object-validatordefinition) object and passing that to [Validator.addValidatorDefinition](#classmethod-validatoraddvalidatordefinition)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [String](#type-string) | false | — | type name for the new validator |
| condition | [ValidatorConditionCallback](#type-validatorconditioncallback) | false | — | callback, function or expression to evaluate to determine whether validation was successful |

### Groups

- validation

### See Also

- [Validator.addValidators](#classmethod-validatoraddvalidators)

**Flags**: A

---
