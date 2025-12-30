# Relations

[← Back to API Index](../reference.md)

---

## KB Topic: Relations

### Description
SmartClient allows relations to be declared between dataSources using the [foreignKey](../classes/DataSourceField.md#attr-datasourcefieldforeignkey) property. Declaring foreign key relations between dataSources enables multiple sophisticated and automatic behaviors.
#### Relation types
There are three types of dataSource relation:

*   **Many-to-one**, where the dataSource at the "child" end of a relationship declares a foreignKey to the dataSource at the "parent" end. The classic example is an OrderItem dataSource declaring a foreignKey relation to the Order dataSource. Another example might be a City dataSource declaring a foreignKey to the Country dataSource
    
    The default editor for Many-to-one relation fields is a [SelectItem](../classes/SelectItem.md#class-selectitem), allowing the user to select a new value for the field from the options available in the related dataSource.
    
*   **One-to-many**, which is the opposite of many-to-one - the foreignKey is declared at the "parent" end. Examples of this kind of relation are simply the opposite of the many-to-one examples.
    
    The default editor for one-to-many relation fields is a [MultiPickerItem](../classes/MultiPickerItem.md#class-multipickeritem), allowing the user to select a new set of values for the field from the options available in the related dataSource.
    
*   **Many-to-many**, where the dataSources at both ends of the relation declare a foreignKey to a third "middle" or "join" dataSource. In a true many-to-many relation, the only information held in the "join" dataSource is the keys of the two related dataSources; if any other information is stored in the "join" dataSource, it is no longer a many-to-many relation but two separate many-to-one relations. An example of a true many-to-many relation would be Employees to Teams: an Employee can be in multiple Teams, and a Team consists of multiple Emloyees
    
    As with one-to-many relation fields, many-to-many fields will show a [MultiPickerItem](../classes/MultiPickerItem.md#class-multipickeritem) as the default editing interface.
    

For completeness, you could add **one-to-one** relations to this list, but in fact they are not particularly interesting. Conceptually, a one-to-one relation is just a many-to-one relation that happens to have only one record at the many end; there are no other special considerations, like there are with the other relation types.
#### Many-to-one relations
Many-to-one relations, where the "child" dataSource declares a foreignKey to the "parent" dataSource, are the simplest type of relation, because they do not involve any requirement to handle multiple related records. For these relations, SmartClient supports simple, code-free inclusion of fields from the parent into the child, with the [includeFrom](../classes/DataSourceField.md#attr-datasourcefieldincludefrom) mechanism. `includeFrom` fields will be automatically included from the parent dataSource whenever data is fetched from the child dataSource

SmartClient does not support updating the "parent" dataSource fields across a many-to-one relation. You can update the relation itself (by updating the `foreignKey`), but any fields that are included from the parent dataSource must be updated with a separate update operation on the parent dataSource

Many-to-one relations are supported for all dataSource types, both the built-in server dataSource types and [clientOnly](../classes/DataSource.md#attr-datasourceclientonly) dataSources. They are also supported without any extra effort with your own custom dataSource implementations on the server

#### One-to-many relations
One-to-many relations, where the "parent" dataSource declares a foreignKey to the "child" dataSource, are more complicated than many-to-one relations because they involve a requirement to handle multiple related records. You designate a one-to-many relation by declaring both the `foreignKey` to the other dataSource and the [multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple) property on the field.

The way this idea of multiple related records is handled varies according to the dataSource type:

*   [JPA](jpaIntegration.md#kb-topic-integration-with-jpa) and [Hibernate](hibernateIntegration.md#kb-topic-integration-with-hibernate) dataSources, in keeping with the underlying ORM ethos, take an _object-based_ approach: the related records are returned as a list of full-formed record objects, and it is possible to update across the relation simply by modifying the properties of the related record(s) and then updating the base record. See the [JPA and Hibernate Relations](jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations) article for more detail of JPA/Hibernate and relations
*   [SQL](sqlDataSource.md#kb-topic-sql-datasources) dataSources take a _relational_ approach: the related records are not returned directly, but rather a list of the key values required to fetch the related records from the related dataSource. Therefore, an additional fetch is needed to fetch the actual related data. Updates are likewise relational: your code provides the "new" list of related keys, and SmartClient modifies the foreignKey values accordingly; no "child" records are created, updated or deleted in this process, the child records are assumed to exist, and here we are just updating the relational information to link to them. Updating the actual data on the child record(s) is done with separate update operation(s) on the child dataSource
*   One-to-many relations are not supported by other dataSource types

#### Many-to-many relations
Many-to-many relations have the same complexities as one-to-many relations - they both involve a requirement to handle multiple related records. In addition, many-to-many relations must manage the existence of an entry in a "join" dataSource. You designate a many-to-many relation by declaring the `foreignKey` to the related dataSource, via the "join" dataSource, and the [multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple) property, on the foreignKey field of one of the dataSources in the many-to-many relation. For example, declaring the `foreignKey` to Teams on the Employee dataSource (note the dots indicating that the relation path to use is EmployeeTeams->Teams):
```
    <field name="teams" multiple="true" foreignKey="EmployeeTeams.Teams.teamId" />
 
```
The way this idea of multiple related records is handled is different according to dataSource type, similar to one-to-many relations:

*   JPA and Hibernate dataSources take the same object-based approach: the related records are returned as a list of full-formed record objects, and it is possible to update across the relation simply by modifying the properties of the related record(s) and then updating the base record
*   SQL dataSources again take a relational approach: instead of the related records, a list of the key values required to fetch the related records from the related dataSource is returned. Updates are also similar to one-to-many relations: your code provides the "new" list of related keys, and SmartClient creates and deletes record in the "join" dataSource as required. No records are created, updated or deleted on the related dataSource in this process. As with one-to-mny relations, updating the actual data on the related record(s) is done with separate update operation(s) on the related dataSource
*   Many-to-many relations are not supported by other dataSource types

### Related

- [JoinType](../reference.md#type-jointype)
- [DataSource.relatedTableAlias](../classes/DataSource.md#attr-datasourcerelatedtablealias)
- [DataSourceField.primaryKey](../classes/DataSourceField.md#attr-datasourcefieldprimarykey)
- [DataSourceField.foreignKey](../classes/DataSourceField.md#attr-datasourcefieldforeignkey)
- [DataSourceField.childrenProperty](../classes/DataSourceField.md#attr-datasourcefieldchildrenproperty)
- [DataSourceField.rootValue](../classes/DataSourceField.md#attr-datasourcefieldrootvalue)
- [DataSourceField.includeFrom](../classes/DataSourceField.md#attr-datasourcefieldincludefrom)
- [DataSourceField.includeVia](../classes/DataSourceField.md#attr-datasourcefieldincludevia)
- [DataSourceField.relatedTableAlias](../classes/DataSourceField.md#attr-datasourcefieldrelatedtablealias)
- [DataSourceField.otherFKs](../classes/DataSourceField.md#attr-datasourcefieldotherfks)
- [DataSourceField.displayField](../classes/DataSourceField.md#attr-datasourcefielddisplayfield)
- [DataSourceField.foreignDisplayField](../classes/DataSourceField.md#attr-datasourcefieldforeigndisplayfield)
- [DataSourceField.joinType](../classes/DataSourceField.md#attr-datasourcefieldjointype)
- [DataSource.childrenField](../classes/DataSource.md#attr-datasourcechildrenfield)

### See Also

- [DataSourceField.foreignKey](../classes/DataSourceField.md#attr-datasourcefieldforeignkey)
- [DataSourceField.multiple](../classes/DataSourceField.md#attr-datasourcefieldmultiple)
- [jpaHibernateRelations](jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations)

---
