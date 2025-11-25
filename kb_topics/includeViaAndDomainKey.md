# Using includeVia with Composite Keys and domainKey

[← Back to API Index](../main.md)

---

## KB Topic: Using includeVia with Composite Keys and domainKey

### Description
In some legacy systems, composite primary keys are used to simulate multi-tenancy, often by including a `domainKey` or a similar field in the key. SmartClient supports this pattern by allowing `includeVia` to work with composite keys.

This usage is generally discouraged in modern development. We strongly recommend using [SmartClient’s transparent multi-tenancy](multiTenancy.md#kb-topic-transparent-multi-tenancy) approach instead, which provides true multi-tenant separation with less complexity and better long-term maintainability.

However, if you're working with an existing legacy system that uses this pattern, `includeVia` can be used to precisely define foreign key paths involving composite keys and indirect relation chains.

The examples below are based on the DataSources shown at the end of this section and are using the same data structure as in the [`includeVia` syntax and behavior](includeViaSyntax.md#kb-topic-includevia-syntax), but with an additional _domainKey_ primary key field added to all DataSources to separate data into logical domains such as "live" and "test". Similarly all examples below also resolve the same relation chain:

```
 Order > Customer (via accountMgrEmployeeNumber) > Employee > Office
 
```
#### Example 1: Full path specified
Explicit composite keys at every step.
```
 includeFrom="Customer.Employee.Office.city"
 includeVia="Order.customerNumber-domainKey:Customer.accountMgrEmployeeNumber-domainKey:Employee.officeCode-domainKey"
 
```
#### Example 2: Partial includeVia with omitted datasource names
Unambiguous field names allow datasource names to be omitted.
```
 includeFrom="Customer.Employee.Office.city"
 includeVia="customerNumber-domainKey:accountMgrEmployeeNumber-domainKey"
 
```
#### Example 3: Minimal includeVia
Only the override for the non-default FK path is needed; the rest is resolved automatically.
```
 includeFrom="Customer.Employee.Office.city"
 includeVia="accountMgrEmployeeNumber-domainKey"
 
```
#### Example 4: Shorter includeFrom with full includeVia
The includeFrom starts mid-chain, but includeVia ensures correct relation chain from the base DataSource.
```
 includeFrom="Employee.Office.city"
 includeVia="Order.customerNumber-domainKey:Customer.accountMgrEmployeeNumber-domainKey:Employee.officeCode-domainKey"
 
```
#### Example 5: Minimal includeFrom and includeVia
System finds shortest valid path from base to target using the provided override.
```
 includeFrom="Office.city"
 includeVia="accountMgrEmployeeNumber-domainKey"
 
```
#### Datasources used in samples:
```
 <DataSource ID="Order" serverType="sql">
     <fields>
         <field name="orderNumber" type="integer" primaryKey="true" />
         <field name="domainKey" type="text" primaryKey="true" foreignKey="Customer.domainKey"/>
         <field name="orderDate" type="date" required="true"/>
         <field name="customerNumber" type="integer" foreignKey="Customer.customerNumber" />
     </fields>
 </DataSource>
 
```
```
 <DataSource ID="Customer" serverType="sql">
     <fields>
         <field name="customerNumber" type="integer" primaryKey="true" />
         <field name="domainKey" type="text" primaryKey="true" foreignKey="Employee.domainKey" />
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
         <field name="domainKey" type="text" primaryKey="true" foreignKey="Office.domainKey"/>
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
         <field name="domainKey" type="text" primaryKey="true" />
         <field name="city" type="text" />
     </fields>
 </DataSource>
 
```

---
