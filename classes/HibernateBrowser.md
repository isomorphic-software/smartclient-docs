# HibernateBrowser Documentation

[← Back to API Index](../reference.md)

---

## Class: HibernateBrowser

*Inherits from:* [Window](Window.md#class-window)

### Description
A component that connects to a Hibernate configuration and displays the currently-mapped entities. It also allows you to view the bean properties of a selected entity, and optionally retrieves and displays the data currently in the corresponding database table.

The HibernateBrowser can also create a SmartClient DataSource from any existing Hibernate mapping.

---
## Attr: HibernateBrowser.title

### Description
A title to show in the header button of the HibernateBrowser's mapping tree.

**Flags**: IR

---
## Attr: HibernateBrowser.mappingTree

### Description
Instance of TreeGrid used to display the Hibernate mappings (beans and properties)

**Flags**: IR

---
## Attr: HibernateBrowser.selectButton

### Description
Instance of Button used to continue once a table has been selected.

**Flags**: IR

---
## Attr: HibernateBrowser.excludeSubstring

### Description
If set, specifies a substring which must NOT exist in an entity name for it to be included in this HibernateBrowser. If this property is set to a List of strings, entity names are excluded if they match any one of the strings. The comparison is case-insensitive.

For example, `excludeSubstring: ["Order", "inv"]` would exclude all the following entity names: "ORDERS", "Inventory", "client\_invoicing"

Note that if you specify both include and exclude criteria and they conflict (ie, according to the criteria you set, an entity should be both included and excluded), exclude wins.

**Flags**: IR

---
## Attr: HibernateBrowser.includeSubstring

### Description
If set, specifies a substring which must exist in an entity name for it to be included in this HibernateBrowser. If this property is set to a List of strings, entity names are included if they match any one of the strings. The comparison is case-insensitive.

For example, `includeSubstring: ["Order", "inv"]` would match all the following entity names: "ORDERS", "Inventory", "client\_invoicing"

**Flags**: IR

---
## Attr: HibernateBrowser.dataGrid

### Description
Instance of ListGrid used to display the actual data in the database table associated with the mapping selected in the [mappingTree](#attr-hibernatebrowsermappingtree).

**Flags**: IR

---
## Method: HibernateBrowser.getResults

### Description
—

---
## Method: HibernateBrowser.getGeneratedDataSource

### Description
Returns the [DataSource](DataSource.md#class-datasource) most recently auto-derived by this HibernateBrowser. This will correspond to the currently-selected class mapping.

---
