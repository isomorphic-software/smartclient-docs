# includeVia syntax

[← Back to API Index](../main.md)

---

## KB Topic: includeVia syntax

### Description
#### Overview
The [includeVia](../classes/DataSourceField.md#attr-datasourcefieldincludevia) attribute is used in conjunction with [includeFrom](../classes/DataSourceField.md#attr-datasourcefieldincludefrom) to resolve ambiguity when multiple foreign keys point to the same related DataSource. It allows you to explicitly specify which foreign key path should be used to retrieve data from the related DataSource.

In its simplest form, includeVia references a single foreign key field, such as:

```
 <field name="salesRepEmployeeNumber" type="integer" foreignKey="Employee.employeeNumber" />
 <field name="salesRepLastName" includeFrom="Employee.lastName" includeVia="salesRepEmployeeNumber" />
 <field name="accountMgrEmployeeNumber" type="integer" foreignKey="Employee.employeeNumber" />
 <field name="accountMgrLastName" includeFrom="Employee.lastName" includeVia="accountMgrEmployeeNumber" />
 
```
In more complex scenarios, where relationships span multiple DataSources or involve composite foreign keys, `includeVia` can define an indirect relation chain — a multi-step path of linked DataSources leading to the target field. This allows precise control over relation resolution, especially when there are multiple possible foreign key paths between DataSources, and you want deterministic control over how relations are resolved, overriding default SmartClient behavior.

For example, to resolve the chain `Order > Customer > Employee > Office`, you can use `includeVia` to specify which foreign keys (single-field or composite) to follow at each step.

#### Syntax
`[dsName.]field1-field2:[dsName.]field3-field4...`

*   `"."` separates a DataSource ID from its field / composite key fields
*   `"-"` separates fields that are part of a composite key
*   `":"` separates relation steps across different DataSources

Datasource names are optional if field names are unambiguous across the chain.
#### Behavior & Rules

*   Each segment must refer to a defined [foreignKey](../classes/DataSourceField.md#attr-datasourcefieldforeignkey) (or listed in [otherFKs](../classes/DataSourceField.md#attr-datasourcefieldotherfks) in the corresponding DataSource.
*   Once `includeVia` is used, the chain must follow the segments as specified, without skipping intermediate DataSources.
*   After the last segment of includeVia, relation detection can proceed using default logic.
*   The same format and rules apply whether keys are single-field or composite.
*   Works identically for both includeVia and queryFK.

#### Composite PK usage notes
Support for composite primary keys in `includeVia` is available, but should be used with caution. While there are valid use cases — such as modeling compound identifiers or many-to-many relationships with additional attributes — the need for composite keys is relatively rare in modern schema design.

Composite keys are most often found in legacy systems, and their use typically reflects limitations or design choices made before more scalable patterns were available. For multi-tenancy specifically, we strongly recommend using [SmartClient’s transparent multi-tenancy](multiTenancy.md#kb-topic-transparent-multi-tenancy) approach, which provides clean tenant separation without duplicating schema or embedding tenancy logic in primary keys.

If you're working with a legacy system and need to preserve existing composite key structures, `includeVia` does support this pattern. For example, some systems use a _domainKey_ or a similar field as part of composite keys to simulate multi-tenancy — this approach is supported, but not recommended for new development. See [includeViaAndDomainKey](includeViaAndDomainKey.md#kb-topic-using-includevia-with-composite-keys-and-domainkey) for more details.

#### Examples
All examples are based on the DataSources shown at the end of this section.

Note that `Customer > Employee` relation can use foreignKey field `accountMgrEmployeeNumber` (Account manager) or foreignKey field `salesRepEmployeeNumber` (Sales representative).

All examples below resolve the same relation chain:

```
 Order > Customer (via accountMgrEmployeeNumber) > Employee > Office
 
```
#### Example 1: Full path specified
Explicit composite keys at every step.
```
 includeFrom="Customer.Employee.Office.city"
 includeVia="Order.customerNumber:Customer.accountMgrEmployeeNumber:Employee.officeCode"
 
```
#### Example 2: Partial includeVia with omitted datasource names
Unambiguous field names allow datasource names to be omitted.
```
 includeFrom="Customer.Employee.Office.city"
 includeVia="customerNumber:accountMgrEmployeeNumber"
 
```
#### Example 3: Minimal includeVia
Only the override for the non-default FK path is needed; the rest is resolved automatically.
```
 includeFrom="Customer.Employee.Office.city"
 includeVia="accountMgrEmployeeNumber"
 
```
#### Example 4: Shorter includeFrom with full includeVia
The includeFrom starts mid-chain, but includeVia ensures correct relation chain from the base DataSource.
```
 includeFrom="Employee.Office.city"
 includeVia="Order.customerNumber:Customer.accountMgrEmployeeNumber:Employee.officeCode"
 
```
#### Example 5: Minimal includeFrom and includeVia
System finds shortest valid path from base to target using the provided override.
```
 includeFrom="Office.city"
 includeVia="accountMgrEmployeeNumber"
 
```
#### Datasources used in samples:
```
 <DataSource ID="Order" serverType="sql">
     <fields>
         <field name="orderNumber" type="integer" primaryKey="true" />
         <field name="orderDate" type="date" required="true"/>
         <field name="customerNumber" type="integer" foreignKey="Customer.customerNumber" />
     </fields>
 </DataSource>
 
```
```
 <DataSource ID="Customer" serverType="sql">
     <fields>
         <field name="customerNumber" type="integer" primaryKey="true" />
         <field name="customerName" type="text" required="true"/>
         <field name="salesRepEmployeeNumber" type="integer" foreignKey="Employee.employeeNumber" />
         <field name="accountMgrEmployeeNumber" type="integer" foreignKey="Employee.employeeNumber" />
     </fields>
 </DataSource>
 
```
```
 <DataSource ID="Employee" serverType="sql">
     <fields>
         <field name="employeeNumber" type="integer" primaryKey="true" />
         <field name="lastName" type="text" required="true"/>
         <field name="firstName" type="text" required="true"/>
         <field name="officeCode" type="text" foreignKey="Office.officeCode" />
     </fields>
 </DataSource>
 
```
```
 <DataSource ID="Office" serverType="sql">
     <fields>
         <field name="officeCode" type="text" primaryKey="true" />
         <field name="city" type="text" />
     </fields>
 </DataSource>
 
```

---
