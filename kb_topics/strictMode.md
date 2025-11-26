# Strict Mode

[← Back to API Index](../reference.md)

---

## KB Topic: Strict Mode

### Description
Enabling "strict mode" means that any attributes in a [Component XML](componentXML.md#kb-topic-component-xml) file which are not declared in [Component Schema](../reference.md#class-componentschema) will cause warnings in the server-side log.

Enabling strict mode can help catch typos in attribute names that may be difficult to spot. However, custom attributes are generally allowed in Component XML and it is not required to declare them in advance in Component Schema, so there are various ways to disable strict mode warnings at fine granularity.

In server.properties, strict mode can be turned on or off system-wide for specific schema or specific attributes of schema. Examples:

```
 # set the global default for *all* Component XML and DataSources
 schema.strict.all:true

 # enable strict checking for any <DataSource> tag
 schema.strict.DataSource:true

 # enable strict checking for DataSource.operationBindings, but not for
 # <OperationBinding> in general (it can appear in other contexts)
 schema.strict.DataSource.operationBindings:true 
 
```
Note that the above settings do not apply to inheriting classes. For example, enabling strict validation for `<DataBoundComponent>` would not enable strict validation for `<ListGrid>` tags.

Strict mode can be disabled for a specific tag by setting strictValidation="false". For example, the following would suppress any warnings for custom attributes that appeared on a particular DataSource's fields:

```
     <DataSource .. />
         <fields strictValidation="false">
             <field customAttribute="someValue" .. />
         </fields>
     </DataSource>
  The following would be a way of adding a custom attribute and suppressing any warnings for
 just that one attribute.
     <DataSource .. />
         <fields>
             <field name="fieldName">
                 <customAttribute strictValidation="false">someValue</customAttribute>
             </field>
         </fields>
     </DataSource>
```

---
