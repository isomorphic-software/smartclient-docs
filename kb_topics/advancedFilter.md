# Advanced Filtering

[← Back to API Index](../reference.md)

---

## KB Topic: Advanced Filtering

### Description
Isomorphic [DataSources](../classes/DataSource_1.md#class-datasource) provide an advanced filtering mechanism for searching data, including a wide range of builtin [search-operators](../reference_2.md#object-operator), which allow searching via simple comparisons like `equals` and `contains` and more complex checks, like `equalsOtherField` and `regex`. You can also add entirely custom search-operators, via DataSource method [addSearchOperator()](../classes/DataSource_1.md#method-datasourceaddsearchoperator).

For a full list of operators, see [OperatorId](../reference.md#type-operatorid).

### Related

- [OperatorValueType](../reference_2.md#type-operatorvaluetype)
- [OperatorId](../reference.md#type-operatorid)
- [DataSource.addSearchOperator](../classes/DataSource.md#classmethod-datasourceaddsearchoperator)
- [DataSource.setTypeOperators](../classes/DataSource.md#classmethod-datasourcesettypeoperators)
- [DataSource.hasCustomTypeOperators](../classes/DataSource.md#classmethod-datasourcehascustomtypeoperators)
- [Operator.condition](../classes/Operator.md#method-operatorcondition)
- [Operator.compareCriteria](../classes/Operator.md#method-operatorcomparecriteria)
- [DataSource.addSearchOperator](../classes/DataSource_1.md#method-datasourceaddsearchoperator)
- [DataSource.getSearchOperator](../classes/DataSource_1.md#method-datasourcegetsearchoperator)
- [DataSource.getTypeOperators](../classes/DataSource_1.md#method-datasourcegettypeoperators)
- [DataSource.setTypeOperators](../classes/DataSource_1.md#method-datasourcesettypeoperators)
- [DataSource.hasCustomTypeOperators](../classes/DataSource_1.md#method-datasourcehascustomtypeoperators)
- [DataSource.getFieldOperators](../classes/DataSource_1.md#method-datasourcegetfieldoperators)
- [DataSource.getFieldDefaultOperator](../classes/DataSource_1.md#method-datasourcegetfielddefaultoperator)
- [DataSource.getFieldOperatorMap](../classes/DataSource_1.md#method-datasourcegetfieldoperatormap)
- [DataSource.getTypeOperatorMap](../classes/DataSource_1.md#method-datasourcegettypeoperatormap)
- [DataSource.evaluateCriterion](../classes/DataSource_2.md#method-datasourceevaluatecriterion)
- [AdvancedCriteria](../reference.md#object-advancedcriteria)
- [Criterion](../reference_2.md#object-criterion)
- [AdvancedCriterionSubquery](../reference.md#object-advancedcriterionsubquery)
- [Operator](../reference_2.md#object-operator)
- [CriterionValues](../reference.md#object-criterionvalues)
- [SimpleType.validOperators](../classes/SimpleType.md#attr-simpletypevalidoperators)
- [SimpleType.defaultOperator](../classes/SimpleType.md#attr-simpletypedefaultoperator)
- [AdvancedCriteria.strictSQLFiltering](../reference.md#attr-advancedcriteriastrictsqlfiltering)
- [AdvancedCriteria._constructor](../reference.md#attr-advancedcriteria_constructor)
- [Criterion.operator](../classes/Criterion.md#attr-criterionoperator)
- [Criterion.fieldName](../classes/Criterion.md#attr-criterionfieldname)
- [Criterion.value](../classes/Criterion.md#attr-criterionvalue)
- [Criterion.criteria](../classes/Criterion.md#attr-criterioncriteria)
- [Criterion.start](../classes/Criterion.md#attr-criterionstart)
- [Criterion.end](../classes/Criterion.md#attr-criterionend)
- [DataSource.allowCriteriaSubqueries](../classes/DataSource_1.md#attr-datasourceallowcriteriasubqueries)
- [Criterion.fieldQuery](../classes/Criterion.md#attr-criterionfieldquery)
- [Criterion.valueQuery](../classes/Criterion.md#attr-criterionvaluequery)
- [Criterion.fieldStaticValue](../classes/Criterion.md#attr-criterionfieldstaticvalue)
- [AdvancedCriterionSubquery.queryOutput](../classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryoutput)
- [AdvancedCriterionSubquery.queryFK](../classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubqueryqueryfk)
- [AdvancedCriterionSubquery.dataSource](../classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerydatasource)
- [AdvancedCriterionSubquery.criteria](../classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerycriteria)
- [AdvancedCriterionSubquery.canEmbedSQL](../classes/AdvancedCriterionSubquery.md#attr-advancedcriterionsubquerycanembedsql)
- [Operator.ID](../classes/Operator.md#attr-operatorid)
- [Operator.title](../classes/Operator.md#attr-operatortitle)
- [Operator.titleProperty](../classes/Operator.md#attr-operatortitleproperty)
- [Operator.textTitle](../classes/Operator.md#attr-operatortexttitle)
- [Operator.textTitleProperty](../classes/Operator.md#attr-operatortexttitleproperty)
- [Operator.fieldTypes](../classes/Operator.md#attr-operatorfieldtypes)
- [Operator.requiresServer](../classes/Operator.md#attr-operatorrequiresserver)
- [Operator.hidden](../classes/Operator.md#attr-operatorhidden)
- [Operator.valueType](../classes/Operator.md#attr-operatorvaluetype)
- [Operator.usageHint](../classes/Operator.md#attr-operatorusagehint)
- [Operator.editorType](../classes/Operator.md#attr-operatoreditortype)
- [Operator.symbol](../classes/Operator.md#attr-operatorsymbol)
- [DataSourceField.validOperators](../classes/DataSourceField.md#attr-datasourcefieldvalidoperators)
- [DataSourceField.defaultOperator](../classes/DataSourceField.md#attr-datasourcefielddefaultoperator)
- [DataSourceField.filterOn](../classes/DataSourceField.md#attr-datasourcefieldfilteron)
- [DynamicForm.allowExpressions](../classes/DynamicForm.md#attr-dynamicformallowexpressions)
- [FormItem.allowExpressions](../classes/FormItem.md#attr-formitemallowexpressions)
- [FormItem.validOperators](../classes/FormItem.md#attr-formitemvalidoperators)
- [FormItem.defaultOperator](../classes/FormItem.md#attr-formitemdefaultoperator)
- [ListGridField.allowFilterExpressions](../classes/ListGridField.md#attr-listgridfieldallowfilterexpressions)
- [ListGrid.allowFilterExpressions](../classes/ListGrid_1.md#attr-listgridallowfilterexpressions)

---
