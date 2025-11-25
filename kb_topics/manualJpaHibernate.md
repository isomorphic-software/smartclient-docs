# Manual JPA & Hibernate Integration

[← Back to API Index](../main.md)

---

## KB Topic: Manual JPA & Hibernate Integration

### Description
In some cases you may not be able to immediately use the built-in JPADataSource or HibernateDataSource. For example, you have pre-existing business logic that already directly calls JPA or Hibernate APIs, and it may seem to be a large task to refactor this logic so that the built-in DataSources can be used.

In this case you can use the overall approach described in [serverDataIntegration](serverDataIntegration.md#kb-topic-server-datasource-integration) to connect to your pre-existing business logic. You will not be leveraging any of the built-in JPA or Hibernate functionality, so the approach and level of effort will be the same as if you were using a non-Hibernate ORM or integrating with entirely custom Java classes.

*This example* shows a Hibernate-based implementation of a custom DataSource that implements support for simple Criteria, sorting and data paging, but not [AdvancedCriteria](../main.md#object-advancedcriteria), [automatic joins](../classes/DataSourceField.md#attr-datasourcefieldincludefrom), automatic transactions or many other features built into HibernateDataSource.

Because these features are very valuable and more features are added to the built-in DataSources all the time, it's recommended that you refactor your code to use the built-in DataSources as soon as you can; refactoring existing business logic as validators, DMIs, or custom DataSources is often easier than it looks.

You can also take the approach of using the built-in DataSources for new entities or entities where there is currently no significant business logic, while continuing to use your existing code where it's non-trivial to refactor.

---
